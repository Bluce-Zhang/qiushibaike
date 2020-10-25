<!-- 聊天页面底部输入框组件 -->
<template>
	<view class="user-chat-bottom common-flex-align-items">
		<input class="input-text" type="text" placeholder="文明发言" v-model="text" />
		<view class="icon iconfont icon-fabu send common-flex-center" @tap="submit()"></view>
	</view>
</template>

<script>
	
	export default {
		props:{
			
		},
		data() {
			return {
				text: ""
			}
		},
		methods:{
			submit(){
				this.$emit("submit",this.text);
				//清空输入框
				this.text = "";
			}
		}
	}
</script>

<style scoped lang="scss">
	.user-chat-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 90rpx;
		padding: 10rpx 20rpx;
		border-top: 1rpx solid #EEEEEE;
		.input-text{
			flex: 1;
			background-color: #F7F7F7;
			padding: 15rpx 15rpx;
			border-radius: 15rpx;
		}
		
		.send{
			width: 100rpx;
			font-size: 45rpx;
		}
	}
</style>
