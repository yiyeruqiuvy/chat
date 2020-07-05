<template>
	<view>
		<view class="news">
			<view class="text1">
				这位朋友，关心啥呢
			</view>
			<br>
			<input class="news_content" v-model="title" placeholder="比如:高考"/>
			<br>
			<button type="default"  @click=search(title) v-on="title">
				一键搜索
			</button>
			比如这些热点：
			<br>
			<view v-for="hotspot in hotspots" :key="hotspot.id">
				{{ hotspot }}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'请在这里输入哦',
				hotspots : []
			}
		},

		onLoad:function(){
			uni.showLoading({
				title:"加载中...."
			});
			uni.request({
				url:"http://api.avatardata.cn/ActNews/LookUp?key=63739504a02245859d6f59b1a56edf47",
				method:"GET",
				data:{},
				success: (res) => {
					this.hotspots = res.data.result;
					uni.hideLoading({
					});
				},
				fail: (res) => {
					alert(res.data.error_code)
				},
				complete: () => {}
			});
		},
		methods: {
			search(title){
				//alert(dream);
				uni.navigateTo({
					url:"./new_content?title="+title
				});
			}
		}
	}
</script>

<style>
.news,button{
	color: #36b8a5;
}
</style>
