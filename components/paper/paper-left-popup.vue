	<!-- 小纸条页面弹窗 -->
<template>
	<view>
		<!-- 操作菜单-->
		<view class="pager-menu-mask" v-show="show" @tap="hidePopup()"></view>
		 <view class="pager-menu" v-show="show">
			 <view hover-class="pager-menu-hover" @tap="addFriend()">
				 <view class="icon iconfont icon-sousuo"></view>
				 加糗友
			 </view>
			 <view hover-class="pager-menu-hover" @tap="clear()">
				 <view class="icon iconfont icon-qingchu"></view>
				 清除未读
			 </view>
		 </view>
	</view>
</template>

<script>
	
	export default {
		props:{
			show:Boolean
		},
		methods:{
			hidePopup(){
				this.$emit('hide');
			},
			addFriend(){
				this.$emit('addFriend');
			},
			clear(){
				this.$emit('clear');
			}
		}
	}
	
</script>

<style scoped lang="scss">
	.pager-menu-mask{
		position: fixed;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		background-color: rgba($color: #000000, $alpha: 0.2);
		z-index: 998;
	}
	
	.pager-menu{
		position: fixed;
		right: 0rpx;
		top: 80rpx;
		background-color: #FFFFFF;
		z-index: 999;
		width: 50%;
		box-shadow: 1rpx 1rpx 20rpx 2rpx #CCCCCC;
		>view{
			padding: 15rpx;
			display: flex;
			align-items: center;
			.icon{
				font-size: 26rpx;
				font-weight: bold;
				margin-right: 20rpx;
			}
		}
	}
	.pager-menu-hover{
		background-color: #EEEEEE;
	}
</style>
