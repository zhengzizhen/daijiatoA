<template>
	<view class="bgcolor pd30">
		<view class="card bor_r">
			<view class="content dis_f jscb">
				<label>数量</label>
				<view class="dis_f">
					<p @click='reduce'>-</p>
					<text>{{num}}</text>
					<p @click='add'>+</p>
				</view>
			</view>

			<view class="content dis_f jscb">
				<label>送货上门</label>
				<view @click="toaddress" class="ipt dis_f alitmc">
					<span>立即填写</span>
					<image src="@/static/image/Promoter/right.jpg" mode=""></image>
				</view>
			</view>

			<view class="content dis_f jscb ">
				<label>电话</label>
				<view class="ipt dis_f alitmc">
					<label>17272727272</label>
					<image src="@/static/image/Promoter/right.jpg" mode=""></image>
				</view>
			</view>
		</view>

		<view class="fixed dis_f jscc">
			<view class="btn">
				提交申请
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				num: 1,
			}
		},
		// 自定义此页面的转发给好友(已经有全局的分享方法，此处会覆盖全局)
		onShareAppMessage(res) {
			return {
				title: '页面分享的标题',
				path: '/pages/Promoter/promotion',
				// imageUrl: '/static/imgs/mylogo.png'
			}
		},
		// 自定义页面的分享到朋友圈
		onShareTimeline(res) {
			return {
				title: '页面分享的标题',
				path: '/pages/Promoter/promotion',
				// imageUrl: '/static/imgs/mylogo.png'
			}
		},
		methods: {
			reduce() {
				if (this.num == 1) {
					return false
				}
				this.num--
			},
			add() {
				this.num++
			},
			toaddress() {
				this.$jump('./address')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.bgcolor {
		padding-top: 50rpx;
	}

	.card {
		box-sizing: border-box;
		width: 690rpx;
		height: auto;
		padding: 0rpx 30rpx;
		background-color: white;

		.content {
			border-bottom: 1px solid #E6E6E6;
			padding: 30rpx 0;

			.ipt {
				span {
					font-size: 30rpx;
					font-weight: 500;
					color: #999999;
					text-align: right;
				}

				image {
					margin-left: 10rpx;
					width: 13rpx;
					height: 23rpx;
				}
			}

			label {
				font-size: 30rpx;
				font-weight: 500;
				color: #222222;
			}

			text {
				padding: 0 20rpx;
				background-color: #F7F7F7;
				height: 56rpx;
				line-height: 56rpx;
				font-size: 30rpx;
				font-weight: 500;
				color: #222222;
			}

			p:nth-child(1) {
				background-color: #F7F7F7;
				width: 56rpx;
				height: 56rpx;
				text-align: center;
				border-radius: 10rpx 0 0 10rpx;
			}

			p:nth-child(3) {
				background-color: #F7F7F7;
				width: 56rpx;
				height: 56rpx;
				text-align: center;
				border-radius: 0 10rpx 10rpx 0;
			}
		}

		.content:nth-child(3) {
			border: none;
		}
	}

	.fixed {
		box-sizing: border-box;
		position: fixed;
		padding-top: 20rpx;
		bottom: 0;
		right: 0;
		width: 750rpx;
		height: 166rpx;
		background: #FFFFFF;
		box-shadow: 0rpx -4rpx 9rpx 0rpx rgba(21, 21, 21, 0.04);
	}
</style>