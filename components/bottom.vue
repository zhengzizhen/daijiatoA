<template>
	<view class="posf">
		<view class="fixed bor_r"></view>
	</view>
</template>

<script>
	export default {
		name: "bottom",
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.posf {
		width: 100%;
		position: fixed;
		bottom: 20rpx;
		left: 0;

		.fixed {
			margin: 0 auto;
			width: 268rpx;
			height: 10rpx;
			background-color: #010101;
		}
	}
</style>