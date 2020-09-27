<!-- 话题详情页面 -->
<template>
	<view>
		<!-- 背景图 -->
		<view class="bg position-relative">
			<image class="image filter" src="../../static/demo/datapic/16.jpg" mode="scaleToFill"></image>
		</view>
		
		<!-- 中部头像和描述 -->
		<view class="middle position-relative">
			<view class="common-flex head-image">
				<image src="../../static/demo/datapic/16.jpg"></image>
				<text>#话题标题#</text>
			</view>
			<view class="common-flex common-flex-align-items info">
				<text>动态:10</text>
				<text>今日:0</text>
			</view>
			<view class="describe">
				<text>话题描述</text>
			</view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad(e) {
			if(e.detail){
				let res = JSON.stringify(e.detail);
				console.log(res);
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss">

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
			text{
				margin: 0rpx 10rpx;
			}
		}
	}

</style>
