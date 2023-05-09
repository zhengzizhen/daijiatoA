<template>
	<view class="pd30 body">
		<view class="dis_f jscb content">
			<p>姓名</p>
			<text>卢本伟</text>
		</view>

		<view class="dis_f jscb content">
			<p>性别</p>
			<text>男</text>
		</view>

		<view class="dis_f jscb content">
			<p>手机号</p>
			<text>17633612613</text>
		</view>
		
		<view class="dis_f jscb content">
			<p>身份证号</p>
			<text>411329199912153118</text>
		</view>
		
		<view class="dis_f jscb content alitmc">
			<p>身份证</p>
			<view class="image"></view>
		</view>
		
		<view class="dis_f jscb content alitmc">
			<p>营业执照</p>
			<view class="image"></view>
		</view>
		
		
		<!-- <view class="fixed">
			<p>听单中</p>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	.body {
		padding-top: 20rpx;
	}

	.content {
		margin: 60rpx 0;
		p{
			font-size: 30rpx;
			font-weight: 500;
			color: #000000;
		}
		text{
			font-size: 30rpx;
			font-weight: 500;
			color: #999999;
		}
		.image{
			width: 344rpx;
			height: 194rpx;
			background: #CCCCCC;
			border-radius: 20rpx;
		}
	}
	.fixed{
		position: fixed;
		bottom: 40rpx;
		right: 40rpx;
		width: 96rpx;
		height: 96rpx;
		border: 2px solid;
		border-radius: 50%;
		border-image: linear-gradient(0deg, #98E05F, #0DE3AC) 10 10;
		background: linear-gradient(0deg, #EAFFF4 0%, #FFFFFF 100%);
		box-shadow: 3rpx 7rpx 6rpx 0rpx rgba(16,155,82,0.05);
	}
</style>