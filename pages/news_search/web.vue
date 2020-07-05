  <template>
	<view>
		
		<view class="content">
			内容：<br>
			{{content}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content:'',
			}
		},
		onLoad:function(res){
			this.content = res.content;
		},
		methods: {
			
		}
	}
</script>

<style>
.content{
	color: #36b8a5;
}
</style>
