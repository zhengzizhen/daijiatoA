<template>
	<view class="pd30 body dis_f flexw jscb">
		<view class="card" v-for="(v,index) in list" :key="index" @click="toMenu(index)">
			<p>{{v.name}}</p>
			<p class="img">
				<image :src="v.image" mode=""></image>
			</p>
		</view>
		<Card />
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
				list: [{
						name: '我的钱包',
						image: '../../static/image/Promoter/money.png'
					},
					{
						name: '我的推广',
						image: '../../static/image/Promoter/teltame.png'
					},
					{
						name: '推广记录',
						image: '../../static/image/Promoter/record.png'
					},
					{
						name: '我的信息',
						image: '../../static/image/Promoter/user.png'
					},
				]
			};
		},
		methods: {
			toMenu(index) {
				switch (index) {
					case 0:
						this.$jump('./myMoney')
						break
					case 1:
						this.$jump('./promotion')
						break
					case 2:
						this.$jump('./take')
						break
					case 3:
						let a = Math.round(Math.random())
						if(a == 0){
							this.$jump('/pages/Service/authentication?tit=','params','推广商身份认证')
							return false
						}else{
							this.$jump('./Information')
						}
						break
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.body {
		padding-top: 60rpx;
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
			color: #0E7741;
		}

		.img {
			position: absolute;
			right: -100rpx;
			bottom: -44rpx;
			width: 240rpx;
			height: 240rpx;
			background: #EAFFF4;
			border-radius: 50%;

			image {
				margin-top: 90rpx;
				margin-left: 40rpx;
				width: 86rpx;
				height: 86rpx;
			}
		}
	}
	.card:nth-child(3) {
		p {
			color: #A95319;
		}

		.img {
			background: #FFEFE5;
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
</style>