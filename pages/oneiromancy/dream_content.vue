<template>
	<view>
		<view class="dream_content" v-for="(dream,index,id) in dreams">
			<view class="title">
				{{dream.title}}:
			</view>
	<!-- 		<rich-text :nodes="Array">
				解梦：{{dream.content}}
			</rich-text> -->
			<text class="dream_content">
				{{dream.content}}
			</text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				dreams : '',
			}
		},
		onLoad:function(dream){
			uni.request({
				url:"http://api.avatardata.cn/ZhouGongJieMeng/LookUp?key=850e5790a9674436a3cf4466b7a0e9b6&keyword=梦见"+dream.dream,
				method:"GET",
				data:{},
				success: (res) => {
					this.dreams = res.data.result;
				},
				fail: (res) => {
					alert(res.data.error_code)
				},
				complete: () => {}
			});
		},
		methods: {
			
		}
	}
</script>

<style>
.dream_content{
	color: #36B8A5;
}
view{
	color: #36B8A5;
	
}
</style>
