<template>
	<view class="pd30 body">
		<p class="title">营业执照</p>
		<view class="cont"  @click="upimage">
			<image v-if="ref" class="img" src="@/static/image/Promoter/xc.png" mode=""></image>
			<image v-else class="ref" :src="img" mode=""></image>
		</view>

		<p class="title mb20">门店照片</p>
		<u-upload :fileList="fileList1" @afterRead="afterRead"  name="1" multiple :maxCount="10">
			<p class="up dis_f jscc alitmc">+</p>
		</u-upload>


		<label class="address dis_f alitmc mt20">
			<image src="@/static/image/Promoter/address.jpg" mode=""></image>
			<p>郑州时代广场</p>
		</label>

		<p class="title">联系方式</p>
		<input class="inpt" type="number" maxlength="11" v-model="user.call" placeholder="输入联系方式">

		<p class="title">门店简介</p>
		<textarea v-model="user.textarea" id="" cols="30" rows="10" placeholder="简单介绍一下吧"></textarea>

		<p class="title">微信收款账号</p>
		<input class="inpt" type="text" v-model="user.phone" placeholder="输入支付宝收款账号">

		<p class="title">收款人姓名</p>
		<input class="inpt" type="text" v-model="user.name" placeholder="输入收款人姓名">

		<view class="btn" @click="submit">
			提交审核
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList1: [],
				user: {
					phone: '',
					textarea: '',
					call: '',
					name: ''
				},
				ref: true,
				img: '',
				imagelist:[],
				promoter:'服务商'
			}
		},
		onLoad() {},
		methods: {
			upimage() {
				uni.chooseImage({
					success: (chooseImageRes) => {
						uni.showLoading({
							title: '上传中'
						})
						const tempFilePaths = chooseImageRes.tempFilePaths;
						uni.uploadFile({
							url: 'http://z.y15926.com/api/upload', //仅为示例，非真实的接口地址
							filePath: tempFilePaths[0],
							name: 'file',
							formData: {
								'user': 'test'
							},
							success: (uploadFileRes) => {
								let img = JSON.parse(uploadFileRes.data).data.path
								this.img = img
								uni.hideLoading()
								this.ref = false
							}
						});
					}
				});
			},
			// 新增图片
			async afterRead(event) {
				// 当设置 multiple 为 true 时, file 为数组格式，否则为对象格式
				let lists = [].concat(event.file)
				let fileListLen = this[`fileList${event.name}`].length
				lists.map((item) => {
					this[`fileList${event.name}`].push({
						...item,
						status: 'uploading',
						message: '上传中'
					})
				})
				for (let i = 0; i < lists.length; i++) {
					const result = await this.uploadFilePromise(lists[i].url)
					let item = this[`fileList${event.name}`][fileListLen]
					this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
						status: 'success',
						message: '',
						url: result
					}))
					fileListLen++
				}
			},
			uploadFilePromise(url) {
				return new Promise((resolve, reject) => {
					let a = uni.uploadFile({
						url: 'http://z.y15926.com/api/upload', // 仅为示例，非真实的接口地址
						filePath: url,
						name: 'file',
						formData: {
							user: 'test'
						},
						success: (res) => {
							setTimeout(() => {
								resolve(res.data.data)
								this.imagelist = this.imagelist.concat(JSON.parse(res.data).data.path)
							}, 1000)
						}
					});
				})
			},
			async submit(){
				if(this.img == ''){
					uni.$u.toast('营业执照不能为空')
					return false
				}else if(this.imagelist == ''){
					uni.$u.toast('门店照片不能为空')
					return false
				}else if(this.user.call == ''){
					uni.$u.toast('联系方式不能为空')
					return false
				}else if(this.user.textarea == ''){
					uni.$u.toast('门店简介不能为空')
					return false
				}else if(this.user.phone == ''){
					uni.$u.toast('微信收款账号不能为空')
					return false
				}else if(this.user.name == ''){
					uni.$u.toast('收款人名字不能为空')
					return false
				}
				const params ={
					store_business_license:this.img,
					store_photo:this.imagelist,
					store_intro:this.user.textarea,
					wx_account:this.user.phone,
					wx_nickname:this.user.name,
					phone:this.user.call,
					prompt:this.promoter
				}
				const res = await this.$http('promoter/store/apply',params)
				uni.$u.toast('申请提交成功，请等待审核')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.body {
		padding-top: 20rpx;
		min-height: 1500rpx;
		height: auto;
		padding-bottom: 150rpx;
	}

	.title {
		font-size: 30rpx;
		font-weight: 500;
		color: #222222;
	}

	.cont {
		margin: 20rpx 0;
		width: 690rpx;
		height: 300rpx;
		line-height: 350rpx;
		background: #F7F8FB;
		border-radius: 20rpx;
		text-align: center;

		.ref {
			width: 690rpx;
			height: 300rpx;
		}

		.img {
			width: 88rpx;
			height: 88rpx;
		}
	}

	.up {
		margin: 0rpx 0;
		background-color: #F7F8FB;
		width: 200rpx;
		height: 200rpx;
		font-size: 100rpx;
		color: #CCCCCC;
		font-weight: normal;
		border-radius: 10rpx;
	}

	.address {
		margin-bottom: 40rpx;

		image {
			width: 17rpx;
			height: 23rpx;
		}

		p {
			margin-left: 10rpx;
			font-size: 24rpx;
			font-weight: 500;
			color: #666666;
		}
	}

	/deep/.input {
		width: 690rpx;
		height: 88rpx;
		margin: 20rpx 0;
		background: #F7F8FB;
		border-radius: 20rpx;
		box-sizing: border-box;
		padding: 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}

	.inpt {
		width: 690rpx;
		height: 88rpx;
		margin: 20rpx 0;
		background: #F7F8FB;
		border-radius: 20rpx;
		box-sizing: border-box;
		padding: 0 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}

	textarea {
		margin: 20rpx 0;
		width: 690rpx;
		height: 210rpx;
		background: #F7F8FB;
		border-radius: 20rpx;
		box-sizing: border-box;
		padding: 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}

	.btn {
		margin-top: 100rpx;
	}

	/deep/.u-upload__button {
		width: 200rpx !important;
		height: 200rpx !important;
	}

	/deep/.u-upload__status {
		width: 200rpx !important;
		height: 200rpx !important;
	}

	/deep/.u-upload__wrap__preview__image {
		width: 200rpx !important;
		height: 200rpx !important;
	}
</style>