<template>
	<view class="news" >
		<news-item @itemClick="goDetail" :list="news"></news-item>
	</view>
</template>

<script>
	import newsItem from '../../components/news-item/news-item.vue'
	export default {
		data() {
			return {
				news:[]
			}
		},
		components:{
			'news-item':newsItem
		},
		methods: {
			getNews(){
				uni.request({
					url:'http://c.m.163.com/nc/article/headline/T1348649580692/0-40.html',
					success: (res) => {
						console.log(res)
						this.news=res.data.T1348649580692
					}
				})
			},
			goDetail(id){
				uni.navigateTo({
					url:'../news-detail/news-detail?id='+id,
				})
				
			}
		},
		onLoad() {
			this.getNews()
		}
	}
</script>

<style lang="scss">
.news{
	
}
</style>
