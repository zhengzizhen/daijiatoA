<template>
	<view class="pd30 body">
		
		<view class="posir ios">
			<image src="@/static/image/Promoter/background.jpg" mode=""></image>
			
			<view class="posia ioss">
				<view class="ct_nav posir">
					<text>我的账户余额(元)</text>
					<p>￥{{userinfo.commission}}</p>
					<view @click.stop="toMoney" class="cashout posia">
						<p>去提现</p>
					</view>
				</view>
			</view>
		</view>
		
		<view class="dis_f flexw jscb">
			<view class="card" v-for="(v,index) in list" :key="index" @click="toMenu(index)">
				<p>{{v.name}}</p>
				<p class="img">
					<image :src="v.image" mode=""></image>
				</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money: 200,
				list: [{
						name: '核销记录',
						image: '../../static/image/Promoter/record.png'
					},
					{
						name: '我的信息',
						image: '../../static/image/Promoter/user.png'
					},
				],
				userinfo:{}
			}
		},
		onLoad() {
			this.getlist()
		},
		methods: {
			getlist(){
				this.userinfo = uni.getStorageSync('userinfo')
			},
			toMoney() {
				this.$jump('/pages/Promoter/Money')
			},
			toDream() {
				this.$jump('./Money')
			},
			toMenu(index) {
				switch (index) {
					case 0:
						this.$jump('./record')
						break;
					case 1:
						this.$jump('/pages/Promoter/Information')
						break;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.body{
		padding-top: 40rpx;
	}
	.ct_nav {
		box-sizing: border-box;
		margin-top: 20rpx;
		width: 100%;
		padding: 60rpx 40rpx;
		height: 286rpx;
		// background: url('@/static/image/Promoter/background.jpg') no-repeat 0 0;
		background-size: 100%;
		box-shadow: 0rpx 10rpx 7rpx 0rpx rgba(73, 202, 164, 0.08);
		border-radius: 20rpx;
		color: white;

		text {
			font-size: 22rpx;
		}

		p {
			font-size: 60rpx;
			font-weight: bold;
		}

		.cashout {
			top: 60rpx;
			right: 0rpx;
			width: 146rpx;
			height: 60rpx;
			line-height: 60rpx;
			text-align: center;
			background: #FFFFFF;
			box-shadow: 3rpx 7rpx 16rpx 0rpx rgba(16, 155, 82, 0.1);
			border-radius: 30rpx 0rpx 0rpx 30rpx;

			p {
				font-size: 30rpx;
				font-weight: 500;
				color: #35C77C;
			}
		}
	}

	.card {
		margin-top: 30rpx;
		width: 335rpx;
		height: 160rpx;
		background: #FFFFFF;
		box-shadow: 1rpx 3rpx 16rpx 0rpx rgba(0, 0, 0, 0.06);
		border-radius: 20rpx;
		box-sizing: border-box;
		position: relative;
		overflow: hidden;
		padding: 20rpx;

		p {
			display: inline-block;
			font-size: 32rpx;
			font-weight: bold;
			color: #A95319;
		}

		.img {
			position: absolute;
			right: -100rpx;
			bottom: -44rpx;
			width: 240rpx;
			height: 240rpx;
			background: #FFEFE5;
			border-radius: 50%;

			image {
				margin-top: 90rpx;
				margin-left: 40rpx;
				width: 86rpx;
				height: 86rpx;
			}
		}
	}

	.card:nth-child(2) {
		p {
			color: #9D1C1F;
		}

		.img {
			background: #FFECED;
		}
	}
	.ios{
		width: 692rpx;
		height: 300rpx;
		image{
			width: 692rpx;
			height: 300rpx;
		}
		.ioss{
			width: 692rpx;
			top: 0;
			left: 0;
		}
	}
</style>