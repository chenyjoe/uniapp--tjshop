<template>
	<view>
		<view class="news_item" @click="navigator(index)" v-for="(item,index) in list" :key="index">
			<image :src="item.imgsrc"></image>
			<view class="right">
				<view class="tit">
					{{item.title}}
				</view>
				<view class="info">
					<text>发表时间：{{item.ptime | formatDate}}</text>
					<text>浏览次数：{{item.replyCount}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['list'],
		filters:{
			formatDate(date){
				const nDate=new Date(date)
				const year=nDate.getFullYear()
				const month=(nDate.getMonth()+1).toString().padStart(2,0)
				const day=nDate.getDate().toString().padStart(2,0)
				return year+'-'+month+'-'+day
			}
		},
		methods:{
			navigator(id){
				this.$emit('itemClick',id)
			}
		}
	}
</script>

<style lang="scss">
.news_item{
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid $shop-color;
		image{
			min-width: 230rpx;
			max-width: 230rpx;
			height: 200rpx;
			
		}
		.right{
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			.tit{
				font-size: 30rpx;
			}
			.info{
				font-size: 24rpx;
				text:nth-child(2){
					margin-left: 30rpx;
				}
			}
		}
		
	}
</style>
