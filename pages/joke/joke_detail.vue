<template>
	<view>
		<view class="content">
			<view class="joke_title">笑话：</view>
			<view class="content">
				{{content}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content :''
			}
		},
		onLoad: function(content){
			//console.log(content.cont);
			this.content = content.cont;
		},
		methods: {
			
		}
	}
</script>

<style>
.joke_title{
	color: #0A98D5;
}
.content{
	color: #7cbb4d;
}
</style>
