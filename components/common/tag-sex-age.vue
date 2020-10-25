<!-- 年龄 性别 小组件 -->
<template>
	<view>
		<view class="icon iconfont common-flex-center age-gender" 
			:class="[sex == 0?'icon-nan':'icon-nv']">{{age}}</view>
	</view>
</template>

<script>
	export default {
		props:{
			sex:Number,
			age:Number
		}
	}
</script>

<style scoped>
	.age-gender{
		background-color: #00ABFF;
		border-radius: 10px;
		padding: 0rpx 10rpx;
		color: #FFFFFF;
		font-size: smaller;
		margin-left: 10rpx;
		line-height: 35rpx;
		height: 35rpx;
	}
	.icon-nv{
		background-color: #FF698D !important;
	}
</style>
