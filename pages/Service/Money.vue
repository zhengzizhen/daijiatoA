<template>
	<view class="pd30">
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
		<p class="title">提现记录</p>
		<view class="tabs dis_f">
			<p @click='cheMenu(index)' :class="curry == index?'green':''" v-for="(v,index) in list" :key="index">{{v}}</p>
		</view>
		
		<view v-show="isShow">
			<view class="dis_f jscb content" v-for="(v,i) in 4" :key="i">
				<view class="lefts">
					<p>提现至银行卡</p>
					<label>2023-09-21 18：00</label>
				</view>
				<view class="right">
					<p class="rigs">-524</p>
					<label>已通过</label>
				</view>
			</view>
		</view>
		
		<view class="dis_f jscb content" v-for="(v,i) in 4" :key="i" v-show="!isShow">
			<view class="lefts">
				<p>提现至银行卡</p>
				<label>2023-09-21 18：00</label>
			</view>
			<view class="right">
				<p>-229</p>
				<label>驳回原因： 银行卡号错误</label>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				money:200,
				curry:0,
				list:['已通过','已驳回'],
				isShow:true,
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
			cheMenu(index){
				if(index == this.curry){
					return false
				}
				this.curry = index
				if(this.curry == 0){
					this.isShow = true
				}else{
					this.isShow = false
				}
			},
			toMoney(){
				this.$jump('/pages/Promoter/Money')
			}
		}
	}
</script>

<style lang="scss" scoped>
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
			right: 1rpx;
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
	.title{
		margin: 20rpx 0;
		font-size: 32rpx;
		font-weight: bold;
		color: #000000;
	}
	.tabs{
		p{
			width: 345rpx;
			height: 74rpx;
			line-height: 74rpx;
			text-align: center;
			background: #E6E6E6;
			color: #999999;
			font-size: 28rpx;
			font-weight: 500;
			color: #999999;
		}
		.green{
			background: #35C77C;
			color: white;
		}
	}
	.content{
		padding: 30rpx 0;
		border-bottom: 1px solid #E6E6E6;
		.lefts{
			p{
				font-size: 28rpx;
				font-weight: 500;
				color: #000000;
			}
			label{
				font-size: 24rpx;
				font-weight: 500;
				color: #999999;
			}
		}
		.right{
			text-align: right;
			p{
				font-size: 30rpx;
				font-weight: 500;
				color: #999999;
			}
			label{
				font-size: 24rpx;
				font-weight: 500;
				color: #FF4040;
			}
			.rigs{
				color: #000000;
			}
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
