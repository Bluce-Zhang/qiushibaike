	<!-- 话题页面话题分类组件 -->
<template>
	<view class="topic-classfiy">
		<!-- 第一行 -->
		<view class="common-flex">
			<view>热门分类</view>
			<view class="common-flex-center more" @click="openMore()">
				<view>更多</view>
				<view class="icon iconfont icon-jinru"></view>
			</view>
		</view>
		<!-- 第二行 -->
		<view class="common-flex-center">
			<block v-for="(item,index) in nav" :key="index">
				<view class="animated fadeInLeft" @click="openDeail(item)">{{item.name}}</view>
			</block>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			nav:Array
		},
		methods:{
			openMore(){
				console.log("更多");
				uni.navigateTo({
					url:"../../pages/topic-nav/topic-nav"
				})
			},
			openDeail(item){
				console.log("打开话题分类页面");
			}
		}
	}
</script>

<style scoped>
	/**
	 * 热门分类的样式
	 */
	.topic-classfiy{
		border-top: 2rpx solid #EEEEEE;
		border-bottom: 2rpx solid #EEEEEE;
		padding: 20rpx 20rpx;
	}
	.topic-classfiy>view:first-child{
		justify-content: space-between;
	}
	
	.topic-classfiy>view:first-child .more>view{
		color: #CFCFCF;
	}
	.topic-classfiy>view:last-child{
		margin-top: 20rpx;
		margin-bottom: 10rpx;
	}
	.topic-classfiy>view:last-child>view{
		flex: 1;
		background-color: #F7F7F7;
		padding: 2rpx 5rpx;
		text-align: center;
		border-radius: 5rpx;
		margin: 0 10rpx;
		color: #9A9A9A;
	}
</style>
