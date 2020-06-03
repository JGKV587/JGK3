<template>
	<view class="news_detail">
		<text class="title">{{detail.title}}</text>
		<view class="info">
			<text>发表时间:{{detail.add_time | formatDate}}</text>
			<text>浏览次数:{{detail.click}}</text>
		</view>
		<view class="content" >
			<rich-text :nodes="detail.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:null,
				detail:{}
			}
		},
		methods: {
			async getNewsDetail(){
				const res = await this.$myRequest({
					url:'/api/getnew/'+this.id
				})
				console.log(res)
				this.detail=res.data.message[0]
			}
		},
		onLoad(s){
			console.log(s)
			this.id=s.id
			this.getNewsDetail()
		}
	}
</script>

<style lang="scss">
.news_detail{
	width: 710rpx;
	font-size: 25rpx;
	padding: 0 20rpx;
	.title{
		font-size: 35rpx;
		text-align: center;
		display: block;
		margin: 20rpx 0;
	}
	.info{
		display: flex;
		justify-content: space-between;
	}
}
</style>
