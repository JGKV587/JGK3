<template>
	<view class="goods_list">
		<goods-list @goodsitemclick="goGoodsDetail" :goods="goods"></goods-list>
		<view v-if="flag" class="isOver">
			------没了------
		</view>
	</view>
</template>

<script>
	import goodslist from'../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pageindex:1,
				goods:[],
				flag:false
			}
		},
		methods: {
			//获取商品列表的数据
			async getgoodslist(callback){
				const res=await this.$myRequest({
					url:'/api/getgoods?pageindex='+this.pageindex
				})
				this.goods=[...this.goods,...res.data.message]
				callback&&callback();
			},
			//导航到商品详情页
			goGoodsDetail(id){
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?id='+id
				})
			}
		},
		onLoad() {
			this.getgoodslist()
		},
		onReachBottom() {
			if(this.goods.length<this.pageindex*10) return this.flag=true
			console.log("触底了")
			this.pageindex++
			this.getgoodslist()
		},
		onPullDownRefresh() {
			console.log('下拉刷新了')
			this.pageindex=1
			this.goods=[]
			this.flag=false
			setTimeout(()=>{
				this.getgoodslist(()=>{
					uni.stopPullDownRefresh()
				})
			},1000)
		},
		components:{
			'goods-list':goodslist
		}
	}
</script>

<style lang="scss">
.goods_list{
	background-color: #eee;
}
.isOver{
	width: 100%;
	height: 50px;
	line-height: 50px;
	text-align: center;
	font-size: 28rpx;
}
</style>
