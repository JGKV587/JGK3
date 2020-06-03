<template>
	<view class="news">
		<news-item @itemClick="goData()" :list='newslist'></news-item>
	</view>
</template>

<script>
	import newsitem from '../../components/new-item/news-item.vue'
	export default {
		data() {
			return {
				newslist:[]
			}
		},
		methods: {
			async getNews(){
				const res = await this.$myRequest({
					url:'/api/getnewslist'
				})
				this.newslist=res.data.message
			},
			goData(id){
				uni.navigateTo({
					url:'/pages/news-detail/news-detail?id='+id
				})
			}
		},
		components:{
			'news-item':newsitem
		},
		onLoad() {
			this.getNews()
		}
	}
</script>

<style lang="scss">
	.news {
		
	}
</style>
