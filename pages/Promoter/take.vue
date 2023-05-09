<template>
	<view class="bgcolor">
		<view class="tabs dis_f" >
			<p :class="curry==index?'green':''" @click="select(index)" v-for="(item,index) in list" :key="index">{{item}}</p>
		</view>
		<view class="card dis_f alitmc posir" v-for="(v,index) in arr" :key="index">
			<view class="img"></view>
			<view class="center">
				<p>订单订单</p>
				<p>推广时间：2023-02-20</p>
			</view>
			<p class="posia" v-if="v.state == 0">进行中</p>
			<p class="posia success" v-if="v.state == 1">已完成</p>
			<p class="posia cancel" v-if="v.state == 2">已取消</p>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: ['进行中', '已完成', '已取消'],
				arr:[],
				curry:null,
				arrlist: [{
					order: '826968643135',
					date: '2023-04-06',
					state: 0,
				},{
					order: '826968643135',
					date: '2023-04-06',
					state: 1,
				},{
					order: '826968643135',
					date: '2023-04-06',
					state: 2,
				}]
			}
		},
		onLoad() {
			this.arr = this.arrlist
		},
		methods: {
			select(index){
				this.curry = index
				this.arr = []
				switch (index){
					case 0:
					this.arrlist.forEach((item,i)=>{
						if(item.state == 0){
							this.arr.push(item)
						}
					})
					break;
					case 1:
					this.arrlist.forEach((item,i)=>{
						if(item.state == 1){
							this.arr.push(item)
						}
					})
					break;
					case 2:
					this.arrlist.forEach((item,i)=>{
						if(item.state == 2){
							this.arr.push(item)
						}
					})
					break;
				}
			}
		}
	}
</script>

<style lang="scss">
	.tabs {
		height: 88rpx;
		line-height: 88rpx;
		background-color: white;
		justify-content: space-around;

		p {
			font-size: 30rpx;
			font-weight: 500;
			color: #222222;
		}
		.green:nth-child(1){
			color:#FF8331
		}
		.green:nth-child(2){
			color:#35C77C
		}
		.green:nth-child(3){
			color:#999999
		}
	}

	.card {
		width: 690rpx;
		height: 170rpx;
		background: #FFFFFF;
		box-sizing: border-box;
		border-radius: 20rpx;
		margin: 20rpx 30rpx;
		padding: 20rpx;

		.img {
			width: 120rpx;
			height: 120rpx;
			background: #999999;
			border-radius: 20rpx;
		}

		.center {
			margin-left: 20rpx;

			p {
				font-size: 30rpx;
				font-weight: 500;
				color: #222222;
			}

			p:nth-child(2) {
				margin-top: 10rpx;
			}
		}

		.posia {
			right: 16rpx;
			top: 16rpx;
			font-size: 26rpx;
			font-weight: 500;
			color: #FF8331;
		}

		.success {
			color: #35C77C !important;
		}

		.cancel {
			color: #999999;
		}
	}
</style>