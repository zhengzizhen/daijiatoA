<template>
	<view class="pd30 body">
		
		<view class="posir ios">
			<image src="@/static/image/Promoter/background.jpg" mode=""></image>
			<view class="posia ioss">
				<view class="ct_nav posir" @click="toDream">
					<text>我的账户余额(元)</text>
					<p>￥{{userinfo.commission}}</p>
					<view @click.stop="toMoney" class="cashout posia">
						<p>去提现</p>
					</view>
				</view>
			</view>
		</view>
		<p class="tit">提现记录</p>
		
		<view class="dis_f content alitmc jscb" v-for="(v,index) in list" :key="index">
			<view class="dis_f flex_c msg">
				<p>{{v.fund_type}}</p>
				<text>{{v.created_at}}</text>
			</view>
			<text class="red">{{v.number}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money: 200,
				list:[
				],
				userinfo:{},
				page:1,
				bottom:false
			}
		},
		onLoad() {
			this.userinfo = uni.getStorageSync('userinfo')
			this.getlog()
		},
		onReachBottom() {
			if(this.bottom == true){
				return false
			}
			this.page+=1
			this.getlog()
		},
		methods: {
			async getlog(){
				const res = await this.$http('promoter/fund/log',{
					page:this.page,
					limit:10,
					type:'withdraw'
				})
				if(res.data.length<10){
					this.bottom = true
				}
				this.list = this.list.concat(res.data)
			},
			toMoney() {
				this.$jump('./Money')
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
		padding: 60rpx 40rpx;
		height: 286rpx;
		// background: url('../../static/image/Promoter/background.jpg') no-repeat 0 0;
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
	.tit{
		margin: 20rpx 0;
		font-size: 32rpx;
		font-weight: bold;
		color: #000000;
	}
	.content{
		margin-top: 20rpx;
		border-bottom: 1px solid #e6e6e6;
		padding-bottom: 20rpx;
		.msg{
			justify-content: center;
			p{
				margin-bottom: 20rpx;
				font-size: 28rpx;
				font-weight: 500;
				color: #000000;
			}
			text{
				font-size: 24rpx;
				font-weight: 500;
				color: #999999;
			}
		}
		.red{
			font-size: 30rpx;
			font-weight: 500;
			color: #FF4040;
		}
	}
	.ios{
		width: 694rpx;
		height: 300rpx;
		image{
			width: 694rpx;
			height: 300rpx;
		}
		.ioss{
			width: 694rpx;
			top: 0;
			left: 0;
		}
	}
</style>