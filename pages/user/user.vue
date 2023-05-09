<template>
	<view class="pd30 body">
		<p class="title">上传身份证</p>
		<view class="dis_f jscb">
			<view class="card dis_f  flex_c jscc alitmc" @click="upimg">
				<view class="bacth">
					<p>+</p>
				</view>
				<text>身份证人面像</text>
			</view>
			<view class="card dis_f flex_c jscc alitmc" @click="upimg">
				<view class="bacth">
					<p>+</p>
				</view>
				<text>身份证国徽面</text>
			</view>
		</view>
		
		<p class="title">收款账号</p>
		<input class="inpt" type="number" maxlength="18" placeholder="输入收款账号" v-model="user.bank">
		
		<p class="title">姓名</p>
		<input class="inpt" type="text" maxlength="6" placeholder="输入你的姓名" v-model="user.name">
		
		<p class="title">手机号</p>
		<input class="inpt" type="number" maxlength="11" placeholder="输入你的手机号" v-model="user.phone">
		
		<view class="btn">
			提交审核
		</view>
		<Card v-if='CardShow' />
	</view>
</template>

<script>
	import Card from '@/components/bottom.vue'
	export default {
		components: {
			Card
		},
		data() {
			return {
				user:{
					bank:'',
					name:'',
					phone:'',
				},
				CardShow:true
			}
		},
		onLoad() {
			let ua = uni.getSystemInfoSync().platform;
			if(ua == 'ios'){
				this.CardShow = false
				return false
			}
			console.log(this.CardShow);
		},
		methods: {
			upimg(){
				uni.chooseImage({
					count: 6, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: function (res) {
						console.log(JSON.stringify(res.tempFilePaths));
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
.body{
	padding-top: 30rpx;
}
.title{
	margin: 20rpx 0;
	font-size: 34rpx;
	font-weight: 500;
	color: #000000;
}
.card{
	width: 335rpx;
	height: 203rpx;
	background: #F7F7F7;
	border-radius: 20rpx;
	.bacth{
		width: 60rpx;
		height: 60rpx;
		line-height: 55rpx;
		border-radius: 50%;
		text-align: center;
		background-color: #B3B3B3;
		p{
			color: white;
			font-size: 48rpx;
		}
	}
	text{
		margin-top: 20rpx;
		font-size: 24rpx;
		font-weight: 500;
		color: #666666;
	}
}
.inpt {
		width: 690rpx;
		height: 88rpx;
		margin: 20rpx 0;
		background: #F7F8FB;
		border-radius: 20rpx;
		box-sizing: border-box;
		padding:0 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}
	.btn{
		margin-top: 400rpx;
	}
</style>
