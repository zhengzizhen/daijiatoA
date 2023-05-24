<template>
	<view class="body">
		<p class="index_title">请选择您的身份</p>
		<text class="label">不同的身份不同的权限</text>

		<view class="card bor_r dis_f alitmc pd30" @click="toService">
			<image src="@/static/image/tuiguang.jpg" mode=""></image>
			<view class="text dis_f flex_c">
				<p>服务商</p>
				<text>扫描核销码是否已使用</text>
			</view>
		</view>

		<view class="card bor_r dis_f alitmc pd30" @click="toPromoter">
			<image src="@/static/image/fuwu.jpg" mode=""></image>
			<view class="text dis_f flex_c">
				<p>推广商</p>
				<text>推广推广</text>
			</view>
		</view>

		<view class="card bor_r dis_f alitmc pd30" @click="toUser">
			<image src="@/static/image/fuwu.jpg" mode=""></image>
			<view class="text dis_f flex_c">
				<p>个人认证</p>
				<text>个人认证</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				promoter: '', //认证类型
			}
		},
		onLoad() {},
		methods: {
			async toPromoter() {
				const res = await this.$http('promoter/detail')
				uni.setStorageSync('userinfo',res.data)
				if (res.data.promoter_status == '审核中') {
					uni.$u.toast('你的认证正在审核中')
					return false
				}
				if (res.data.promoter == '推广商') {
					this.$jump('/pages/Promoter/home')
					return false
				} else if (res.data.promoter == null) {
					this.$jump('/pages/Service/authentication?name=', 'params', '推广商')
					return false
				}
				uni.$u.toast('您的身份是' + res.data.promoter)
			},
			async toService() {
				const res = await this.$http('promoter/detail')
				uni.setStorageSync('userinfo',res.data)
				if (res.data.promoter_status == '审核中') {
					uni.$u.toast('你的认证正在审核中')
					return false
				}
				if (res.data.promoter == '服务商') {
					this.$jump('/pages/Service/home')
					return false
				} else if (res.data.promoterr == '') {
					this.$jump('/pages/Service/authentication?name=', 'params', '服务商')
					return false
				}
				uni.$u.toast('您的身份是' + res.data.promoter)
			},
			async toUser() {
				const res = await this.$http('promoter/detail')
				uni.setStorageSync('userinfo',res.data)
				if (res.data.promoter_status == '审核中') {
					uni.$u.toast('你的认证正在审核中')
					return false
				}
				if (res.data.promoter == '个人') {
					this.$jump('/pages/Promoter/home')
					return false
				} else if (res.data.promoterr == '') {
					this.$jump('/pages/user/user')
					return false
				}
				uni.$u.toast('您的身份是' + res.data.promoter)
			}
		},
	}
</script>

<style lang="scss" scoped>
	.body {
		min-height: 1500rpx;
		height: auto;
		background: linear-gradient(180deg, #9EE9C3 0%, #FFFFFF 100%);
		padding: 200rpx 30rpx 30rpx 30rpx;

		.index_title {
			font-size: 50rpx;
			font-weight: bold;
			color: #010101;
			margin: 10rpx 0;
		}

		.label {
			font-size: 30rpx;
			font-weight: 500;
			color: #666666;
		}

		.card {
			height: 220rpx;
			background: #FFFFFF;
			margin: 30rpx auto;

			image {
				width: 163rpx;
				height: 163rpx;
			}

			.text {
				margin-left: 40rpx;
				justify-content: center;

				p {
					margin-bottom: 30rpx;
					font-size: 36rpx;
					font-weight: bold;
					color: #222222;
				}

				text {
					font-size: 24rpx;
					font-weight: 500;
					color: #666666;
				}
			}
		}
	}
</style>