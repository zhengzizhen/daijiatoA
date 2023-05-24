<template>
	<view class="pd30 body">
		<p class="title">上传身份证</p>
		<view class="dis_f jscb">
			<view v-if="front" class="card dis_f  flex_c jscc alitmc" @click="upimg">
				<view class="bacth">
					<p>+</p>
				</view>
				<text>身份证人面像</text>
			</view>
			<image v-else class="card" :src="frontimg" mode=""></image>
			<view v-if="size" class="card dis_f flex_c jscc alitmc" @click="upimg1">
				<view class="bacth">
					<p>+</p>
				</view>
				<text>身份证国徽面</text>
			</view>
			<image v-else class="card" :src="siteimg" mode=""></image>
		</view>

		<p class="title">收款账号</p>
		<input class="inpt" type="text" maxlength="18" placeholder="输入收款账号" v-model="user.bank">

		<p class="title">姓名</p>
		<input class="inpt" type="text" maxlength="6" placeholder="输入你的姓名" v-model="user.name">

		<p class="title">手机号</p>
		<input class="inpt" type="number" maxlength="11" placeholder="输入你的手机号" v-model="user.phone">

		<view class="btn" @click="submit">
			提交审核
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				user: {
					bank: '',
					name: '',
					phone: '',
				},
				CardShow: true,
				frontimg: '',
				siteimg: '', //
				front: true,
				size: true
			}
		},
		onLoad() {
			console.log(this.CardShow);
		},
		methods: {
			upimg() { //正面
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
								this.frontimg = img
								uni.hideLoading()
								this.front = false
							}
						});
					}
				});
			},
			upimg1() { //反面
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
								this.siteimg = img
								uni.hideLoading()
								this.size = false
							}
						});
					}
				});
			},
			async submit() {
				const reg = /^1((34[0-8])|(8\d{2})|(([35][0-35-9]|4[579]|66|7[35678]|9[1389])\d{1}))\d{7}$/

				if (this.frontimg == '') {
					uni.$u.toast('身份证正面不能为空')
					return false
				} else if (this.siteimg == '') {
					uni.$u.toast('身份证反面不能为空')
					return false
				} else if (this.user.bank == '') {
					uni.$u.toast('收款账号不能为空')
					return false
				} else if (this.user.name == '') {
					uni.$u.toast('姓名不能为空')
					return false
				} else if (this.user.phone == '') {
					uni.$u.toast('手机号不能为空')
					return false
				} else if (!reg.test(this.user.phone)) {
					uni.$u.toast('请输入正确的手机号')
					return false
				}
				const res = await this.$http('promoter/detail/apply', {
					id_card_front_img: this.frontimg,
					id_card_verso_img: this.siteimg,
					wx_account: this.user.bank,
					wx_nickname: this.user.name,
					phone: this.user.phone
				})
				
				setTimeout(()=>{
					uni.navigateBack()
				},500)
				
				uni.$u.toast('申请提交成功，请耐心等待审核')
			},
		}
	}
</script>

<style lang="scss" scoped>
	.body {
		padding-top: 30rpx;
	}

	.title {
		margin: 20rpx 0;
		font-size: 34rpx;
		font-weight: 500;
		color: #000000;
	}

	.card {
		width: 335rpx;
		height: 203rpx;
		background: #F7F7F7;
		border-radius: 20rpx;

		.bacth {
			width: 60rpx;
			height: 60rpx;
			line-height: 55rpx;
			border-radius: 50%;
			text-align: center;
			background-color: #B3B3B3;

			p {
				color: white;
				font-size: 48rpx;
			}
		}

		text {
			margin-top: 20rpx;
			font-size: 24rpx;
			font-weight: 500;
			color: #666666;
		}
	}

	.inpt {
		width: 100%;
		height: 88rpx;
		margin: 20rpx 0;
		background: #F7F8FB;
		border-radius: 20rpx;
		box-sizing: border-box;
		padding: 0 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}

	.btn {
		margin: 0 auto;
		margin-top: 400rpx;
	}
</style>