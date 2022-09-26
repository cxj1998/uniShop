<template>
	<view>
		<!-- 轮播图 -->
		<u-swiper :list="slides" name="img_url" height="320"></u-swiper>

		<view class="u-text-center u-m-t-30">
			<!-- tabs标签 -->
			<u-tabs :list="sortList" bar-width="100" item-width="160" :current="currentSort" @change="changeSort">
			</u-tabs>
		</view>

		<u-row gutter="16">
			<u-col span="6" v-for="item in goods">
				<goods-card :item="item"></goods-card>
			</u-col>
		</u-row>
		<!-- <u-loading-icon mode="circle" inactive-color="red"></u-loading-icon> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sortList: [{
						name: '默认'
					},
					{
						name: '销量'
					},
					{
						name: '推荐'
					},
					{
						name: '最新'
					},
				],
				currentSort: 0,
				goods: [],
				slides: [],
				page: 1
			}
		},
		onLoad() {
			this.getData()
		},
		methods: {
			changeSort(index) {
				console.log(index);
				this.currentSort = index
				// 重置数据和分页
				this.goods = []
				this.page = 1
				this.getData()
			},
			async getData() {
				const params = {
					page: this.page
				}
				// 增加排序条件
				if (this.currentSort === 1) params.sales = 1
				if (this.currentSort === 2) params.recommend = 1
				if (this.currentSort === 3) params.new = 1
				const res = await this.$u.api.index(params)
				this.goods = [...this.goods, ...res.goods.data]
				this.slides = res.slides
			}
		},
		onReachBottom() {
			this.page = this.page + 1
			this.getData()
		}
	}
</script>

<style lang="scss" scoped>

</style>
