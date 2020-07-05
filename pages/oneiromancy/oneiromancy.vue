<template>
	<view>
		<view class="dream">
			<view class="text1">
				据说小哥昨晚做了个不太明了梦？
			</view>
			<br>
			<input class="dream_content" v-model="dream" placeholder="比如:小狗狗"/>
			<br>
			<view class="text1">
				让小秋来为你解梦吧
			</view>
			<br>
			<button type="default"  @click=jiemeng(dream) v-on="dream">
				解梦
			</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				dream:'请在这里输入哦'
			}
		},
		methods: {
			jiemeng(dream){
				//alert(dream);
				uni.navigateTo({
					url:"./dream_content?dream="+dream
				});
			}
			
		}
	}
</script>

<style>
view{
	color: #36B8A5;
}
button{
	color: #36B8A5;
}
</style>
