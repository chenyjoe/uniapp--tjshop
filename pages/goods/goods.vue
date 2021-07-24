<template>
	<view class="goods_list">
		<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pagenum:30,
				goods:[]
				
			}
		},
		components:{
			"goods-list":goodsList
		},
		methods: {
			goGoodsDetail(id){
				uni.navigateTo({
					url:'../goods-detail/goods-detail?id='+id
				})
			},
			getGoods(){
				uni.request({
					url:'https://api-hmugo-web.itheima.net/api/public/v1/goods/search',
					data:{
						pagenum:this.pagenum
					},
					success: (res) => {
						console.log(res)
						this.goods=[...this.goods,...res.data.message.goods]
					}
				})
			}
		},
		onLoad() {
			this.getGoods()
		},
		onReachBottom() {
			this.pagenum++
			this.getGoods()
		},
		onPullDownRefresh() {
			this.pagenum=30
			this.goods=[]
			setTimeout(()=>{
				this.getGoods()
				uni.stopPullDownRefresh()
			},1000)
			
		}
	}
</script>

<style lang="scss">
.goods_list{
	background: #eee;
}

</style>
