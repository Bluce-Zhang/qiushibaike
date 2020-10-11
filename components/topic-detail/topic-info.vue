<!-- 帖子信息组件 -->
<template>
	<view>
		<!-- 背景图 -->
		<view class="bg position-relative">
			<image class="image filter" :src="info.titlepic" mode="scaleToFill"></image>
		</view>
		
		<!-- 中部头像和描述 -->
		<view class="middle position-relative">
			<view class="common-flex head-image">
				<image :src="info.titlepic"></image>
				<text>#{{info.title}}#</text>
			</view>
			<view class="common-flex common-flex-align-items info">
				<text>动态:{{info.totalnum}}</text>
				<text>今日:{{info.todaynum}}</text>
			</view>
			<view class="describe">
				<text>{{info.desc}}</text>
			</view>
		</view>
	</view>
	
</template>

<script>
	
	export default {
		props:['info']
	}
	
</script>

<style scoped lang="scss">
	
	.image{
		width: 100%;
		height: 300rpx;
	}
	/**
	 * 图片模糊效果
	 */
	.filter{
		filter: blur(3px);
	}
	
	.middle{
		z-index: 10;
		background-color: #FFFFFF;
		padding: 0rpx 20rpx;
		.head-image{
			image{ 
				height: 150rpx;
				width: 150rpx;
				border-radius: 5px;
				margin-top: -75rpx;
			}
			text{
				margin-left: 20rpx;
			}
		}
		
		.info,.describe{
			color: #666666;
		}
		
		.info{
			margin-top: 10rpx;
			text{
				margin: 0rpx 10rpx;
			}
		}
		
		.describe{
			padding-bottom: 20rpx;
			text{
				margin: 0rpx 10rpx;
			}
		}
	}
	
</style>
