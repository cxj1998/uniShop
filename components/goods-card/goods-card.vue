<template>
	<navigator class="goods-item">
		<u-image width="100%" height="300rpx" :src="item.cover_url" />
		<view class="title u-line-1">{{item.title}}</view>
		<view class="u-flex u-row-between">
			<view class="price">￥ {{item.price}}</view>
			<view class="sales">销量：{{item.sales}}</view>
		</view>
	</navigator>
</template>

<script>
	export default {
		name: "goods-card",
		props: {
			item: {
				type: Object,
				default () {
					return {}
				}
			}
		},
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss" scoped>
	.goods-item {
		padding: 40rpx;
		margin-top: 30rpx;
		box-shadow: 0 12rpx 20rpx 0 rgba(0, 0, 0, 0.3);

		.title {
			margin: 10rpx 0;
			font-weight: 500;
			font-size: 32rpx;
		}

		.price {
			color: red;
		}

		.sales {
			color: #888;
		}
	}
</style>
