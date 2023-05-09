<template>
	<view class="pd30 body">
		<p class="title">营业执照</p>
		<u-upload :fileList="fileList6" @afterRead="afterReads" @delete="deletePics" name="6" multiple :maxCount="1"
			width="250" height="150">
			<view class="cont">
				<image class="img" src="@/static/image/Promoter/xc.png" mode=""></image>
			</view>
		</u-upload>

		<p class="title mb20">门店照片</p>
		<u-upload :fileList="fileList1" @afterRead="afterRead" @delete="deletePic" name="1" multiple :maxCount="10">
			<p class="up dis_f jscc alitmc">+</p>
		</u-upload>
		<label class="address dis_f alitmc mt20">
			<image src="@/static/image/Promoter/address.jpg" mode=""></image>
			<p>郑州时代广场</p>
		</label>

		<p class="title">联系方式</p>
		<input class="inpt" type="text" v-model="user.call" placeholder="输入联系方式">

		<p class="title">门店简介</p>
		<textarea v-model="user.textarea" id="" cols="30" rows="10" placeholder="简单介绍一下吧"></textarea>

		<p class="title">支付宝收款账号</p>
		<input class="inpt" type="text" v-model="user.phone" placeholder="输入支付宝收款账号">

		<p class="title">收款人姓名</p>
		<input class="inpt" type="text" v-model="user.name" placeholder="输入收款人姓名">

		<view class="btn">
			提交审核
		</view>

		<Card />
	</view>
</template>

<script>
	import Card from '@/components/bottom.vue'
	export default {
		components: {
			Card
		},
		data() {
			return {
				fileList1: [],
				fileList6: [],
				user: {
					phone: '',
					textarea: '',
					call: '',
					name: ''
				}
			}
		},
		onLoad(option) {
			uni.setNavigationBarTitle({
				title:option.tit
			})
		},
		methods: {
			// 删除图片
			deletePics(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
			},
			// 新增图片
			async afterReads(event) {
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
			// uploadFilePromises(url) {
			// 	return new Promise((resolve, reject) => {
			// 		let a = uni.uploadFile({
			// 			url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
			// 			filePath: url,
			// 			name: 'file',
			// 			formData: {
			// 				user: 'test'
			// 			},
			// 			success: (res) => {
			// 				setTimeout(() => {
			// 					resolve(res.data.data)
			// 				}, 1000)
			// 			}
			// 		});
			// 	})
			// },

			// 删除图片
			deletePic(event) {
				this[`fileList${event.name}`].splice(event.index, 1)
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
						url: 'http://192.168.2.21:7001/upload', // 仅为示例，非真实的接口地址
						filePath: url,
						name: 'file',
						formData: {
							user: 'test'
						},
						success: (res) => {
							setTimeout(() => {
								resolve(res.data.data)
							}, 1000)
						}
					});
				})
			},
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
	/deep/.input{
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
		padding:0 20rpx;
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