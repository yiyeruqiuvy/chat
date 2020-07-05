<template>
	<view>
		<view class="news_content" v-for="(news,index) in newss">
			<image class="image" :src="news.img" mode="aspectFit"></image>
			<view class="title" @click="open(news.content)">	
				{{news.title}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newss : '',
			}
		},
		onLoad:function(title){
			uni.request({
				url:"http://api.avatardata.cn/ActNews/Query?key=63739504a02245859d6f59b1a56edf47&keyword="+title.title,
				method:"GET",
				data:{},
				success: (res) => {
					this.newss = res.data.result;
				},
				fail: (res) => {
					alert(res.data.error_code)
				},
				complete: () => {}
			});
		},
		methods: {
			open(res){
				uni.navigateTo({
					url:"./web?content="+res
				})
			}
		}
	}
</script>

<style>
.image{
	height: 300rpx;
	width: 300rpx;
}
view{
	color: #36b8a5;
}
</style>
