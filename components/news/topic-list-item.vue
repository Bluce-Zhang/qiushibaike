<!-- 话题页面 话题列表条目 -->
<template>
	<view class="topic-list-item common-flex" @click="open()">
		<image :src="item.titlepic" mode="widthFix" lazy-load></image>
		<view class="info">
			<view>#{{item.title}}#</view>
			<view>{{item.desc}}</view>
			<view>动态{{item.totalnum}} 今日{{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object
		},
		methods:{
			open(){
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail?detail='+JSON.stringify(this.item)
				});
			}
		}
	}
</script>

<style scoped>
	/**
	 * 话题列表条目样式
	 */
	.topic-list-item{
		margin-top: 20rpx;
		padding-bottom: 20rpx;
		border-bottom: 1rpx solid #EEEEEE;
	}
	.topic-list-item>image{
		width: 200rpx !important;
		height: 200rpx !important;
		border-radius: 20rpx;
		margin-right: 20rpx;
	}
	.topic-list-item>.info>view{
		color: #BBBBBB;
		font-weight: 300;
	}
	.topic-list-item>.info>view:first-child{
		font-size: 35rpx;
		color: #000000;
	}
</style>
