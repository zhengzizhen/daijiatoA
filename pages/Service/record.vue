<template>
	<view class="pd30 body">
		<view class="date dis_f alitmc" @click="isShow=true">
			<p @click='isShow= true'>{{year}}年{{month}}月{{day}}日</p>
			<image src="@/static/image/Promoter/down.jpg" mode=""></image>
		</view>

		<view class="content dis_f alitmc" v-for="(item,index) in 4" :key="index">
			<image src="@/static/image/fuwu.jpg" mode=""></image>
			<view class="tent">
				<p>芜湖起飞</p>
				<view class="dis_f flex_c">
					<text>核销内容内容内容</text>
					<text>2023-05-06</text>
				</view>
			</view>
		</view>
		<u-picker itemHeight='80' cancelText='取消' confirmColor='#35C77C' :show="isShow" ref="uPicker" :columns="columns"
			@confirm="confirm" @change="changeHandler"></u-picker>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'picker-view',
				years: [],
				year: '',
				months: [],
				month: '',
				days: [],
				day: '',
				value: [9999, this.month - 1, this.day - 1],
				isShow: false,
				indicatorStyle: `height: 50px;`,
				columns: []
			}
		},
		onLoad() {
			this.getpacker()
		},
		methods: {
			getpacker(){
				const date = new Date()
				const years = []
				this.year = date.getFullYear()
				const months = []
				this.month = date.getMonth() + 1
				const days = []
				this.day = date.getDate()
				for (let i = 1990; i <= date.getFullYear(); i++) {
					this.years.push(i + '年')
				}
				for (let i = 1; i <= 12; i++) {
					this.months.push(i + '月')
				}
				for (let i = 1; i <= 31; i++) {
					this.days.push(i + '日')
				}
				this.columns.push(this.years)
				this.columns.push(this.months)
				this.columns.push(this.days)
			},
			changeHandler(e) {
				const {
					columnIndex,
					index,
					// 微信小程序无法将picker实例传出来，只能通过ref操作
					picker = this.$refs.uPicker
				} = e
				if (columnIndex === 0) {
					this.loading = true
					// 模拟网络请求
					uni.$u.sleep(1500).then(() => {
						picker.setColumnValues(1, this.columnData[index])
						this.loading = false
					})
				}
			},
			// 回调参数为包含columnIndex、value、values
			confirm(e) {
				console.log(e);
				this.year = e.value[0].replace('年','')
				this.month = e.value[1].replace('月','')
				this.day = e.value[2].replace('日','')
				this.isShow = false
			}
		}
	}
</script>

<style lang="scss" scoped>
	.body {
		padding-top: 40rpx;
	}

	.date {
		image {
			width: 16rpx;
			height: 9rpx;
			margin-left: 10rpx;
		}

		p {
			font-size: 24rpx;
			font-weight: 500;
			color: #222222;
		}
	}

	.content {
		border-bottom: 1px solid #E6E6E6;
		padding: 30rpx 0;

		.tent {
			margin-left: 40rpx;
		}

		image {
			width: 86rpx;
			height: 86rpx;
		}

		p {
			font-size: 30rpx;
			font-weight: 500;
			color: #222222;
			margin-bottom: 10rpx;
		}

		text {
			font-size: 24rpx;
			font-weight: 500;
			color: #666666;
		}
	}

	.picker-view {
		width: 750rpx;
		height: 600rpx;
		margin-top: 20rpx;
	}

	.item {
		line-height: 100rpx;
		text-align: center;
	}

	.pos {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		min-height: 1500rpx;
		height: auto;
		// background-color: rgba(0,0,0,.5);
	}

	.swip {
		position: fixed;
		bottom: 0;
		right: 0;
	}

	/deep/.u-picker {
		border-radius: 20rpx 20rpx 0 0 !important;
		height: 600rpx;
	}

	/deep/.u-popup__content {
		border-radius: 20rpx 20rpx 0 0 !important;
	}

	/deep/.u-picker__view__column__item {
		font-size: 28rpx;
		font-weight: 500;
		color: #666666;
	}
</style>