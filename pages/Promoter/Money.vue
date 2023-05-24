<template>
	<view class="pd30 body">
		
		
		
		<view class="posir ios">
			<image src="@/static/image/Promoter/background.jpg" mode=""></image>
			<view class="posia ioss">
				<view class="ct_nav posir" @click="toDream">
					<text>我的账户余额(元)</text>
					<p>￥{{userinfo.commission}}</p>
				</view>
			</view>
		</view>
		<view class="dis_f jscb ct_header">
			<p>提现金额</p>
			<p class="red" @click='all'>全部提现</p>
		</view>
		<view class="ct_background dis_f">
			<label>￥</label>
			<input type="digit" maxlength="8" placeholder="请输入提现金额" v-model="tmoney">
		</view>
		<p class="grsed">选择提现方式</p>

		<view class="uni-list">
			<radio-group @change="radioChange">
				<label class="dis_f jscb ct_radio" v-for="(item, index) in items" :key="item.value">
					<view class="dis_f io">
						<image :src="item.image" mode=""></image>
						<text>{{item.name}}</text>
					</view>
					<view>
						<radio color='#FF4040' style="transform:scale(0.8)" :value="item.value"
							:checked="index === current" />
					</view>
				</label>
			</radio-group>
		</view>

		<button class="btn" @click="cashout()"><text>确定提现</text></button>
		<u-popup :round="10" :show="isShow" mode="center" @close="close" @open="open">
			<view class="ct_pop dis_f flex_c">
				<image @click="close()" class="close" src="@/static/image/Promoter/close.png" mode=""></image>
				<image class="success" src="@/static/image/Promoter/success.jpg" mode=""></image>
				<text>申请成功！</text>
			</view>
		</u-popup>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tmoney: '',
				isShow:false,
				items: [
					{
						value: 'Bank',
						name: '微信提现',
						image: '../../static/image/Promoter/yhk.jpg'
					},
				],
				current: 0,
				userinfo:{}
			};
		},
		onLoad() {
			this.userinfo = uni.getStorageSync('userinfo')
		},
		methods: {
			all() {
				this.tmoney = this.userinfo.commission
			},
			radioChange: function(evt) {
				
			},
			async cashout() {
				if(this.tmoney == ''){
					uni.$u.toast('提现金额不能为空')
					return false
				}
				
				const res = await this.$http('promoter/withdraw',{
					money:this.tmoney
				})
				this.getlist()
				this.isShow = !this.isShow
			},
			async getlist(){
				const res = await this.$http('promoter/detail')
				uni.setStorageSync('userinfo',res.data)
				setTimeout(()=>{
					uni.redirectTo({
						url:'/pages/Promoter/myMoney'
					})
				},1000)
			},
			open(){
				
			},
			close() {
				this.isShow = !this.isShow
			},
			// toBank(){
			// 	this.isShow1 = !this.isShow1
			// 	this.$jump('./addBank')
			// },
			tobindUser(){
				
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
	}

	.ct_header {
		margin: 20rpx 0;
		align-items: center;

		.red {
			color: #FF4040;
			font-size: 22rpx;
		}

	}

	.ct_background {
		height: 88rpx;
		background: #F7F7F7;
		align-items: center;

		label {
			margin-left: 30rpx;
			font-size: 36rpx;
			font-weight: bold;
			color: #222222;
		}

		input {
			margin-left: 20rpx;
			font-size: 36rpx;
			font-weight: bold;
			color: #222222;
		}
	}

	.rsed {
		margin: 10rpx 0 30rpx;
		font-size: 22rpx;
		font-weight: 500;
		color: #FF4040;
	}
	.grsed{
		margin: 60rpx 0 40rpx;
		font-size: 30rpx;
		font-weight: 500;
	}

	.ct_radio {
		margin: 20rpx 0;
		align-items: center;
		height: 50rpx;
		line-height: 50rpx;

		.io {
			align-items: center;

			text {
				font-size: 28rpx;
			}
		}

		image {
			display: inline-block;
			width: 40rpx;
			height: 40rpx;
			margin-right: 20rpx;
		}
	}

	.btn {
		margin-top: 608rpx;
	}
	.ct_pop{
		box-sizing: border-box;
		width: 570rpx;
		height: 420rpx;
		background: #FFFFFF;
		border-radius: 20rpx;
		padding: 20rpx 30rpx;
		justify-content: center;
		align-items: center;
		position: relative;
		.success{
			width: 129rpx;
			height: 129rpx;
			margin-bottom: 40rpx;
		}
		.close{
			position: absolute;
			right: 0;
			top: -30rpx;
			width: 20rpx;
			height: 20rpx;
		}
	}
	.bank{
		height: 360rpx;
		.banktit{
			margin: 40rpx auto;
			text-align: center;
			font-size: 34rpx;
			font-weight: 500;
			color: #222222;
		}
		image{
			width: 44rpx;
			height: 44rpx;
		}
		.bankcontent{
			margin-top: 20rpx;
			padding-top: 20rpx;
			border-top: 1px solid #e6e6e6;
			text{
				margin-left: 20rpx;
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
			top: 0;
			left: 0;
		}
	}
</style>