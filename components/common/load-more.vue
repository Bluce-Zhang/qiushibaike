	<!-- 列表底部加载更多组件 -->
<template>
	<view>
		<view class="load-more">{{loadText}}</view>
	</view>
</template>

<script>
	export default {
		props:{
			loadText:String
		}
	}
</script>

<style scoped>
.load-more{
	text-align: center;
	padding: 20rpx;
	color: #AAAAAA;
}
</style>
