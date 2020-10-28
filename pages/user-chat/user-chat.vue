<!-- 聊天页面 -->
<template>
	<view>
		
		<!-- 聊天列表 -->
		<view class="user-chat-list common-flex user-chat-me">
			<image src="../../static/demo/userpic/10.jpg" mode="widthFix" lazy-load></image>
			<view class="user-chat-list-body common-flex-center">
				<!-- <text>内容</text> -->
				<image src="../../static/demo/1.jpg" mode="widthFix" lazy-load></image>
			</view>
		</view>
		<!-- 底部输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
		
	</view>
</template>

<script>
	import userChatBottom from '@/components/user-chat/user-chat-bottom.vue';
	
	export default {
		components: {
			userChatBottom
		},
		data() {
			return {
				
			};
		},
		methods:{
			submit(data){
				console.log("发送:"+data);
			}
		}
	}
</script>

<style lang="scss">

	.user-chat-list{
		
	}
	.user-chat-list>image{
		width: 100rpx;
		height: 100rpx;
		border-radius: 100%;
		flex-shrink: 0;
	}

	.user-chat-list-body{
		position: relative;
		background-color: #F4F4F4;
		padding: 20rpx;
		border-radius: 20rpx;
		margin-left: 20rpx;
		margin-right: 100rpx;
	}
	// 小三角
	.user-chat-list-body::after{
		position: absolute;
		left: -30rpx;
		right: 0;
		top: 30rpx;
		content: '';
		width: 0;
		height: 0;
		border: 20rpx solid #F4F4F4;
		border-color: transparent #F4F4F4 transparent transparent;
		
		
	}
	
	.user-chat-list-body>image{
		max-width: 250rpx;
		max-height: 250rpx;
	}
	
	.user-chat-me{
		// justify-content: flex-end;
		flex-direction: row-reverse;
	}
	
	.user-chat-me>image{
		
	}
	
	.user-chat-me .user-chat-list-body{
		margin-right: 20rpx;
		margin-left: 100rpx;
	}
	
	.user-chat-me .user-chat-list-body:after{
		left: auto;
		right: -20px;
		border-color: transparent transparent transparent #F4F4F4;
	}
	
	
</style>
