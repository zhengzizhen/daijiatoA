<template>
	<view class="pd30 body">
		<view class="dis_f jscb content" v-if="list.wx_nickname">
			<p>姓名</p>
			<text>{{list.wx_nickname}}</text>
		</view>

		<!-- <view class="dis_f jscb content">
			<p>性别</p>
			<text>男</text>
		</view> -->

		<view class="dis_f jscb content" v-if="list.phone">
			<p>手机号</p>
			<text>{{list.phone}}</text>
		</view>
		
		<view class="dis_f jscb content" v-if="list.wx_account">
			<p>微信账号</p>
			<text>{{list.wx_account}}</text>
		</view>
		
		<view class="dis_f jscb content" v-if="list.wx_nickname">
			<p>微信实名</p>
			<text>{{list.wx_nickname}}</text>
		</view>
		
		<view class="dis_f jscb content" v-if="list.store_intro">
			<p>门店简介</p>
			<text>{{list.store_intro}}</text>
		</view>
		
		<view class="dis_f jscb content alitmc" v-if="list.id_card_front_img">
			<p>身份证正面</p>
			<image class="image" :src="list.id_card_front_img" mode=""></image>
		</view>
		
		<view class="dis_f jscb content alitmc" v-if="list.id_card_verso_img">
			<p>身份证反面</p>
			<image class="image" :src="list.id_card_verso_img" mode=""></image>
		</view>
		
		<view class="dis_f jscb content alitmc" v-if="list.store_business_license">
			<p>营业执照</p>
			<image class="image" :src="list.store_business_license" mode=""></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:{}//信息
			}
		},
		onLoad() {
			this.getlist()
		},
		methods: {
			async getlist(){
				const res = await this.$http('promoter/detail')
				this.list = res.data
			}
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