<template>
	<view class="body pd30">
		<p class="tit">门店简介</p>
		<textarea class="textarea bor_r" placeholder="简单介绍一下吧" v-model="content" cols="30" rows="10"></textarea>
		
		<p class="tit">收款账号</p>
		<!-- <input class="bor_r" placeholder-class="placeholder" type="number" maxlength="18" v-model="account" placeholder="请输入收款账号"> -->
		 <u--input
		    placeholder="请输入收款账号"
		    border="surround"
		    v-model="account"
		  ></u--input>
		<view class="btn" @click="toindex">
			提交审核
		</view>
		<Card />
	</view>
</template>

<script>
	import Card from '@/components/bottom.vue'
	export default {
		components:{
			Card
		},
		data() {
			return {
				content:'',
				account:''
			}
		},
		methods: {
			toindex(){
				// if(this.content == ''){
				// 	uni.$u.toast('门店介绍不能为空')
				// 	return false
				// }else if(this.account == ''){
				// 	uni.$u.toast('收款账号')
				// 	return false
				// }
				this.$jump('/pages/index/index')
			}
		}
	}
</script>

<style lang="scss" scoped>
	input{
		font-family: 'PF'
	}
.body{
	padding: 30rpx;
	.tit{
		font-size: 30rpx;
		font-weight: 500;
		color: #222222;
	}
	.textarea{
		margin: 20rpx 0;
		width: 690rpx;
		height: 210rpx;
		background: #F7F8FB;
		box-sizing: border-box;
		padding: 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}
	input{
		margin: 20rpx 0;
		width: 690rpx;
		height: 88rpx;
		background: #F7F8FB;
		box-sizing: border-box;
		padding: 20rpx;
		font-size: 30rpx;
		font-weight: 500;
	}
	.btn{
		margin-top: 880rpx;
	}
}
</style>
