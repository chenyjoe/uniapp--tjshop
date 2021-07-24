<template>
	<view class="goods_detail">
		<swiper indicator-dots>
			<swiper-item v-for="(item,index) in info.pics" :key="index">
				<image :src="item.pics_mid_url"></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text>￥{{info.goods_price}}</text>
				<text>￥{{Number(info.goods_price*1.2).toFixed(0)}}</text>
			</view>
			<view class="goods_name">
				{{info.goods_name}}
			</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>货号：{{info.goods_id}}</view>
			<view>库存：{{info.goods_number}}</view>
		</view>
		<view class="line"></view>
		<view class="box3">
			<view class="tit">详情介绍</view>
			<view class="content">
				<rich-text :nodes="info.goods_introduce"></rich-text>
			</view>
		</view>
		<view class="goods_nav">
			<uni-goods-nav :fill="true"  :options="options" :buttonGroup="buttonGroup"  @click="onClick" @buttonClick="buttonClick" />
		</view>
	</view>
</template>

<script>
import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		data() {
			return {
				id:0,
				info:{},
		        options: [{
		            icon: 'headphones',
		            text: '客服'
		        }, {
		            icon: 'shop',
		            text: '店铺',
		            info: 2,
		            infoBackgroundColor:'#007aff',
		            infoColor:"red"
		        }, {
		            icon: 'cart',
		            text: '购物车',
		            info: 2
		        }],
		        buttonGroup: [{
		          text: '加入购物车',
		          backgroundColor: '#ff0000',
		          color: '#fff'
		        },
		        {
		          text: '立即购买',
		          backgroundColor: '#ffa200',
		          color: '#fff'
		        }
		        ]		
			}
		},
		components: {uniGoodsNav},
		methods: {
			getSwipers(){
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/goods/detail',
					data:{
						goods_id:this.id
					},
					success: (res) => {
						this.info=res.data.message
					}
				})
			},
		      onClick (e) {
		        uni.showToast({
		          title: `点击${e.content.text}`,
		          icon: 'none'
		        })
		      },
		      buttonClick (e) {
		        console.log(e)
		        this.options[2].info++
		      }	
			
		},
		onLoad(options) {
			this.id=options.id
			console.log(options.id)
			this.getSwipers()
		}
	}
</script>

<style lang="scss">
.goods_detail{
	swiper{
		height: 700rpx;
		image{
			width: 100%;
			height: 100%;
		}
	}
	.box1{
		padding: 10px;
		.price{
			font-size: 35rpx;
			color: #b50e03;
			line-height: 80rpx;
			text:nth-child(2){
				color: #ccc;
				font-size: 28rpx;
				margin-left: 20rpx;
				text-decoration: line-through;
			}
		}
		.goods_name{
			font-size: 32rpx;
			line-height: 60rpx;
		}
	}
	.line{
		height: 10rpx;
		width: 750rpx;
		background: #eee;
	}
	.box2{
		padding: 0 10px;
		font-size: 32rpx;
		line-height: 70rpx;
	}
	.box3{
		padding-bottom: 50px;
		.tit{
			color: $shop-color;
			text-align: center;
			font-size: 35rpx;
			border-bottom: 1px solid #eee;
			line-height: 70rpx;
		}
		.content{
			padding: 10px;
			font-size: 30rpx;
			color: #333;
		}
	}
	.goods_nav{
		position: fixed;
		bottom: 0;
		width: 100%;
	}
}
</style>
