<template>
	<view class="contact">
			<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg" mode=""></image>
		<view class="info">
			<view @click="phone">联系电话：400-618-9090(点击拨打)</view>
			<view>联系地址:广东省广州市番禺区1号</view>
		</view>
		<map class="map" :markers="markers" :longitude="longitude" :latitude="latitude" :scale="scale"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:113.329407,
				latitude:23.018367,
				scale:14,
				markers:[
					{
						longitude:113.329407,
						latitude:23.018367,
						iconPath:'/static/zuobiao.jpg',
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber:'400-618-9090'
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact {
		.img {
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx  20rpx;
			font-size: 30rpx;
			view{
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map{
			height: 750rpx;
			width: 750rpx;
		}
	}
</style>
