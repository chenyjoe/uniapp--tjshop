<template>
	<view class="contact">
		<image class="img" src="../../static/R-C.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：15898551576（点击拨打）</view>
			<view>联系地址：湖南省长沙市天心区韶山南路498号中南林业科技大学</view>
		</view>
		<map :scale="scale" :longitude="longitude" :latitude="latitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude:112.997216,
				latitude:28.132978,
				scale:13,
				markers:[
					{
						longitude:112.997216,
						latitude:28.132978,
						iconPath:'../../static/dingwei.png',
						width:30,
						height:30
					}
				]
			}
		},
		methods: {
			phone(){
				uni.makePhoneCall({
					phoneNumber:'15898551576'
				})
			}
		}
	}
</script>

<style lang="scss">
.contact{
	.img{
		width: 750rpx;
		height: 320rpx;
	}
	.info{
		padding: 10rpx 20rpx;
		font-size: 30rpx;
		view{
			line-height: 70rpx;
			border-bottom: 1px solid #eee;
		}
	}
	map{
		width: 750rpx;
		height: 750rpx;
	}
}
</style>
