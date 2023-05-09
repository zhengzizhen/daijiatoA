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
		<Card />
	</view>
</template>

<script>
	import Card from '@/components/bottom.vue'
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {

		},
		methods: {
			toPromoter(){
				this.$jump('/pages/Promoter/home')
			},
			toService(){
				this.$jump('/pages/Service/home')
			},
			toUser(){
				this.$jump('/pages/user/user')
			}
		},
		components:{
			Card
		}
	}
</script>

<style lang="scss" scoped>
	.body{
		min-height: 1500rpx;
		height: auto;
		background: linear-gradient(180deg, #9EE9C3 0%, #FFFFFF 100%);
		padding: 200rpx 30rpx 30rpx 30rpx;
		.index_title{
			font-size: 50rpx;
			font-weight: bold;
			color: #010101;
			margin: 10rpx 0;
		}
		.label{
			font-size: 30rpx;
			font-weight: 500;
			color: #666666;
		}
		.card{
			height: 220rpx;
			background: #FFFFFF;
			margin: 30rpx auto;
			image{
				width: 163rpx;
				height: 163rpx;
			}
			.text{
				margin-left: 40rpx;
				justify-content: center;
				p{
					margin-bottom: 30rpx;
					font-size: 36rpx;
					font-weight: bold;
					color: #222222;
				}
				text{
					font-size: 24rpx;
					font-weight: 500;
					color: #666666;
				}
			}
		}
	}
</style>
