<template>
	<view class="container">
		<view class="content" v-for="(joke,index,id) in jokes" :key = "index" @click="nav(joke.content)">
			笑话 {{id+1}}:
			</br>
			{{joke.content}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				jokes:{}
			}
		},
		onLoad:function(){
			uni.request({
				url:" http://api.avatardata.cn/Joke/QueryJokeByTime?key=dab1189573ff4b6ca62531f51826bcff&page=1&rows=10&sort=asc&time=1418745237",
				method:"GET",
				data:{},
				success: (request) => {
					this.jokes = request.data.result;
					//alert(request.data);
					//console.log(request.data.result);
				},
				fail: (request) => {
					alert(request.data.error_code);
				},
				complete: () => {}
			})
		},
		methods: {
			nav(cont){
				var cont = cont;
				uni.navigateTo({
					url:"./joke_detail?cont="+cont
				});
			}
		},
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.content{
		color: #2d9fb6;
		padding: 5rpx 2rpx;
		margin-bottom: 25rpx;
	}
</style>
