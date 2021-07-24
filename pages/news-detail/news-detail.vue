<template>
	<web-view :src="news[id].url"></web-view>
</template>

<script>
	export default {
		data() {
			return {
				news:[],
				id:0
			}
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
			}
		},
		onLoad(options) {
			console.log(options.id)
			this.id=options.id
			this.getNews()
		}
	}
</script>

<style lang="scss">

</style>
