<template>
	<view class="home">
		<swiper indicator-dots	circular>
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<image :src="item.image_src"></image>
			</swiper-item>
		</swiper>
		<!-- 导航 -->
		<view class="nav">
			<view @click="navItemClick(item.path)" class="nav_item" v-for="(item,index) in navs" :key="index">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
			
		</view>
		
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list @goodsItemClick="goGoodsDetail()" :goods="goods"></goods-list>
		</view>
		
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				swipers:[],
				goods:[],
				navs:[
					{
						icon:'iconfont icon-ziyuan',
						title:'甜酒超市',
						path:'/pages/goods/goods'
					},
					{
						icon:'iconfont icon-guanyuwomen',
						title:'联系我们',
						path:'/pages/contact/contact'
					},
					{
						icon:'iconfont icon-tupian',
						title:'图片资料',
						path:'/pages/pics/pics'
					},
					{
						icon:'iconfont icon-shipin',
						title:'视频资料',
						path:'/pages/video/video'
					}
				]
				
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		components:{
			"goods-list":goodsList
		},
		methods: {
			navItemClick(url){
				uni.navigateTo({
					url
				})
			},
			getSwipers () {
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata',
					success: (res) => {
						console.log(res)
						this.swipers=res.data.message
					}
				})
				
			},
			getHotGoods(){
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/goods/search',
					data:{
						pagenum:7
					},
					success: (res) => {
						console.log(res)
						this.goods=res.data.message.goods
					}
				})
				
			},
			goGoodsDetail(id){
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
			}
			
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background: #ffaa00;
					border-radius: 60rpx;
					margin: 10rpx auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 60rpx;
				}
				text{
					font-size: 30rpx;
				}
			}

		}
		.hot_goods{
			background: #eee;
			overflow: hidden;
			margin-top: 10rpx;
			.tit{
				height: 50px;
				line-height: 50px;
				color: #b50e03;
				text-align: center;
				letter-spacing: 20px;
				background: #fff;
				margin: 7rpx 0;
			}
			.goods_list{
				padding: 0 15rpx;
				display: flex;
				flex-wrap: wrap;
				justify-content: space-between;
				.goods_item{
					background: #fff;
					width: 355rpx;
					margin: 10rpx 0;
					padding: 15rpx;
					box-sizing: border-box;
					image{
						width: 80%;
						height: 300rpx;
						display: block;
						margin: auto;
					}
					.price{
						color:#b50e03 ;
						font-size: 36rpx;
						margin: 20rpx 0 5rpx 0;
						text:nth-child(2){
							color: #ccc;
							font-size: 28rpx;
							margin-left: 17rpx;
							text-decoration: line-through;
							
						}
					}
					.name{
						font-size: 28rpx;
						line-height: 50rpx;
						padding:10rpx ;
					}
				}
			}
			
		}
	}
	
</style>
