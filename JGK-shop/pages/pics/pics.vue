<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view v-for="item,index in cates" @click="leftClick(index,item.id)"
			 :key="item.id" :class="active===index?'active':''">{{item.title}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view v-for="item in secondData"  :key="item.id" class="item">
				<image @click="imgdj(item.img_url)" :src="item.img_url" mode=""></image>
				<text>{{item.title}}</text>
			</view>
			<text v-if="secondData.length===0">暂无数据</text>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates:[],
				active:0,
				secondData:[]
			}
		},
		methods: {
			async getPicsCate(){
				const res = await this.$myRequest({
					url:'/api/getimgcategory'
				})
				this.cates=res.data.message
				this.leftClick(0,this.cates[0].id)
			},
			async leftClick(index,id){
				this.active=index
				const res = await this.$myRequest({
					url:'/api/getimages/'+id
				})
				this.secondData=res.data.message
			},
			imgdj(current){
				const urls=this.secondData.map(item=>{
					return item.img_url
				})
				console.log(urls)
				uni.previewImage({
					urls,
					current
				})
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
page{
	height: 100%;
	.pics{
		display: flex;
		height: 100%;
		.left{
			width: 200rpx;
			height: 100%;
			border-right:1px solid #eee;
		}
		view{
			height: 60px;
			line-height: 60px;
			color: #333;
			text-align: center;
			font-size: 30rpx;
			border-top: 1px solid #eee;
		}
		.active{
			background-color: #F0AD4E;
			color: #fff;
		}
		.right{
			height: 100%;
			width: 520rpx;
			margin: 10rpx auto;
			.item{
				image{
					width: 520rpx;
					height: 520rpx;
				}
			}
		}
	}
}
</style>
