<template>
	<view class="bgcolor pd30">
		<view class="card bor_r">
			<view class="content dis_f">
				<label>姓名</label>
				<input type="text" v-model="user.site_username" placeholder="请填写真实姓名">
			</view>
			
			<view class="content dis_f">
				<label>手机号</label>
				<input type="number" maxlength="11" v-model="user.site_phone" placeholder="请填写手机号">
			</view>
			
			<view class="content dis_f">
				<label>省市区</label>
				<input type="text" v-model="user.site_district" placeholder="请输入省市区">
			</view>
			
			<view class="content dis_f">
				<label>详细地址</label>
				<input type="text" v-model="user.site_address" placeholder="请输入详细地址">
			</view>
		</view>
		
		<view class="btn" @click="toPro">
			保存并使用
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user:{
					site_username:'',
					site_phone:'',
					site_district:'',
					site_address:''
				}
			}
		},
		onLoad(option) {
			if(option.obj){
				this.user = JSON.parse(option.obj)
			}
		},
		methods: {
			async toPro(){
				let reg = /^1((34[0-8])|(8\d{2})|(([35][0-35-9]|4[579]|66|7[35678]|9[1389])\d{1}))\d{7}$/
				if(this.user.name == ''){
					uni.$u.toast('姓名不能为空')
					return false
				}else if(this.user.phone == ''){
					uni.$u.toast('手机号不能为空')
					return false
				}else if(this.user.address == ''){
					uni.$u.toast('地址不能为空')
					return false
				}else if(this.user.none == ''){
					uni.$u.toast('详细地址不能为空')
					return false
				}else if(reg.test(this.phone)){
					uni.$u.toast('请输入正确的手机号码')
					return false
				}
				uni.showLoading()
				const res = this.$http('promoter/address/set',this.user)
				uni.hideLoading()
				uni.$u.toast('保存成功')
				setTimeout(()=>{
					this.$jump('/pages/Promoter/promotion','redirect')
				},500)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.bgcolor{
		padding-top: 40rpx;
	}
	.card {
		box-sizing: border-box;
		width: 690rpx;
		height: auto;
		padding: 0rpx 30rpx;
		background-color: white;
	}
	.content {
		border-bottom: 1px solid #E6E6E6;
		padding: 30rpx 0;
		label {
			width: 160rpx;
			font-size: 30rpx;
			font-weight: 500;
			color: #222222;
		}
		input{
			font-size: 30rpx;
			font-weight: 500;
			color: #000000;
		}
	}
	.content:nth-child(4){
		border: none;
	}
	.btn{
		margin-top: 100rpx;
	}
</style>