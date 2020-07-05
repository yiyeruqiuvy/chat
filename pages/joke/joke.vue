<template>
	<view class="container">
		<view class="content" v-for="(joke,index,id) in dataList" :key = "index" @click="nav(joke.content)">
			笑话 {{id+1}}:
			</br>
			{{joke.content}}
		</view>
		<text class="loading-text">
				{{loadingType === 0 ? contentText.contentdown : (loadingType === 1 ? contentText.contentrefresh : contentText.contentnomore)}}
		</text>
	</view>
</template>
<script>
	// export default {
	// 	data() {
	// 		return {
	// 			jokes:{},
	// 		}
	// 	},
	// 	onLoad:function(){
	// 		uni.request({
	// 			url:" http://api.avatardata.cn/Joke/QueryJokeByTime?key=dab1189573ff4b6ca62531f51826bcff&page=1&rows=10&sort=asc&time=1418745237",
	// 			method:"GET",
	// 			data:{},
	// 			success: (request) => {
	// 				this.jokes = request.data.result;
	// 				//alert(request.data);
	// 				//console.log(request.data.result);
	// 			},
	// 			fail: (request) => {
	// 				alert(request.data.error_code);
	// 			},
	// 			complete: () => {}
	// 		})
	// 	},
	// 	methods: {
	// 		nav(cont){
	// 			var cont = cont;
	// 			uni.navigateTo({
	// 				url:"./joke_detail?cont="+cont
	// 			});
	// 		}
	// 	},
	// }
	var page = 1;
	export default {
		data() {
			return {
				dataList:{},
				/* 上拉刷新 */
				loadingType: 0,
				contentText: {
					contentdown: "上拉显示更多",
					contentrefresh: "正在加载...",
					contentnomore: "没有更多数据了"
				},
			}
		},
		onLoad() {
			this.getListInfo();
		},
		/*下拉刷新*/
		onPullDownRefresh: function() {
			this.getListInfo();
		},
		/*上拉刷新*/
		onReachBottom:function(){
			this.getMoreListInfo()
		},
		methods: {
			getListInfo(){
				const that = this;
				page =1
				uni.request({
					url:'http://api.avatardata.cn/Joke/QueryJokeByTime?key=dab1189573ff4b6ca62531f51826bcff&page=1&rows=10&sort=asc&time=1418745237',
					method:'GET',
					data:{
						page:page
					},
					success(res) {
						that.dataList = res.data.result
						uni.hideNavigationBarLoading();
						uni.stopPullDownRefresh();	//得到数据后停止下拉刷新
					}
				})
			},
			/* 上拉加载 */
			getMoreListInfo(){
				const that = this;
				page++;
				
				if (that.loadingType != 0) {
					return false; //loadingType!=0;直接返回
				}
				that.loadingType = 1;
				uni.showNavigationBarLoading();
				uni.request({
					url:'http://api.avatardata.cn/Joke/QueryJokeByTime?key=dab1189573ff4b6ca62531f51826bcff&page=1&rows=10&sort=asc&time=1418745237',
					method:'GET',
					data:{
						page:page
					},
				   success(res) {
						if(that.dataList.length == res.data.count){ //当之前的数据长度等于count时跳出函数，不继续执行下面语句
							that.loadingType = 2;
							uni.hideNavigationBarLoading();//关闭加载动画
							return false;
						}
						that.dataList = that.dataList.concat(res.data.result)
						that.loadingType = 0;//将loadingType归0重置
						uni.hideNavigationBarLoading();//关闭加载动画
				   }
				})
			},
			nav(cont){
				uni.navigateTo({
					url:"./joke_detail?cont="+cont
				});
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.content{
		color: #b43e25;
		padding: 5rpx 2rpx;
		margin-bottom: 25rpx;
	}
	.loading-text{
		height: 80upx;
		line-height: 80upx;
		font-size: 25upx;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}
</style>
