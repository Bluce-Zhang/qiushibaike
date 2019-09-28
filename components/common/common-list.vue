	<!-- 列表的条目 -->
<template>
	<!-- 列表条目 -->
	<view class="common-list common-flex animated bounceIn">
		<!-- 左边 -->
		<view class="common-list-left">
			<image :src="item.userpic" mode="widthFix"></image>
		</view>
		<!-- 右边 -->
		<view class="common-list-right">
			<!-- 昵称和关注 -->
			<view class="common-flex">
				<view class="common-flex-align-items name">
					{{item.username}}
					<view class="icon iconfont common-flex-center age-gender" :class="[item.sex == 0?'icon-nan':'icon-nv']">{{item.age}}</view>
				</view>
				
				<view v-show="!isguanzhu" class="common-flex-center focus" @tap="guanzhu()">+关注</view>
			</view>
			<!-- 标题 -->
			<view>
				{{item.title}}
			</view>
			<!-- 图片 -->
			<view class="common-flex-center">
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix"></image>
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playInfo">{{item.video.looknum}} 次播放 {{item.video.long}}</view> 
				</template>
				
				<template v-if="item.share">
					<!-- 分享的样式 -->
					<view class="common-list-share common-flex-align-items">
						<image :src="item.share.titlepic" mode="widthFix"></image>
						<view>{{item.share.title}}</view>
					</view>
				</template>
				
			</view>
			<!-- 地点  转发 赞 评论 -->
			<view class="common-flex-align-items">
				<view class="location">{{item.path}}</view>
				<view class="common-flex-align-items info">
					<view class="icon iconfont icon-zhuanfa">{{item.sharenum}}</view>
					<view class="icon iconfont icon-pinglun1">{{item.commentnum}}</view>
					<view class="icon iconfont icon-dianzan1">{{item.goodnum}}</view>
				</view>
			</view>
		</view>
	</view>
	
</template>

<script>
	export default {
		props:{
			item:Object,
			index:Number
		},
		data() {
			return {
				isguanzhu:this.item.isguanzhu
			}
		},
		methods:{
			guanzhu(){
				this.isguanzhu = true;
				uni.showToast({
					title:"关注成功"
				});
			}
		}
	}
</script>

<style scoped>
	/**
	 * 列表条目样式
	 */
	.common-list{
		padding: 20rpx 20rpx;
	}
	
	.common-list-left{
		
	}
	.common-list-left>image{
		width: 80rpx;
		height: 80rpx;
		border-radius: 50%;
	}
	.common-list-right{
		flex-flow: 1;
		padding: 0 10rpx;
		border-bottom: 1px solid #EEEEEE;
		padding-bottom: 10rpx;
	}
	/*第一行左右布局*/
	.common-list-right>view:nth-child(1){
		justify-content: space-between;
	}
	.common-list-right>view:nth-child(1) .name{
		color: #9A9A9A;
		font-size: 30rpx;
	}
	.common-list-right>view:nth-child(1) .age-gender{
		background-color: #00ABFF;
		border-radius: 10px;
		padding: 0rpx 10rpx;
		color: #FFFFFF;
		font-size: smaller;
		margin-left: 10rpx;
		line-height: 35rpx;
		height: 35rpx;
	}
	.common-list-right>view:nth-child(1) .focus{
		background-color: #EFEFEF;
		border-radius: 10rpx;
		font-size: smaller;
		padding: 0 15rpx;
	}
	/*第二行标题*/
	.common-list-right>view:nth-child(2){
		font-size: 34rpx;
		padding: 15rpx 0;
	}
	/*第三行图片*/
	.common-list-right>view:nth-child(3){
		position: relative;
		margin-bottom: 10rpx;
	}
	
	.common-list-play,.common-list-playInfo{
		position: absolute;
		color: #FFFFFF;
	}
	.common-list-play{
		font-size: 110rpx;
	}
	.common-list-playInfo{
		right: 30rpx;
		bottom: 10rpx;
		background-color: rgba(51, 51, 51, 0.70);
		border-radius: 15rpx;
		padding: 0px 20rpx;
		font-size: smaller;
	}
	
	.common-list-right>view:nth-child(3)>image{
		border-radius: 20rpx;
	}
	
	/*第4行*/
	.common-list-right>view:nth-child(4){
		justify-content: space-between;
		color: #BBBBBB;
	}
	.common-list-right>view:nth-child(4) .info view{
		padding: 0 8rpx;
	}
	
	/**
	 * 分享样式
	 */
	.common-list-share{
		background-color: #F7F7F7;
		width: 100%;
		padding: 15rpx;
		border-radius: 15rpx;
	}
	
	.common-list-share>image{
		width: 200rpx;
		height: 150rpx !important;
		margin-right: 15rpx;
		border-radius: 10rpx;
	}
</style>
