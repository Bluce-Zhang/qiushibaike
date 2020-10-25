<!-- 聊天页面 -->
<template>
	<view>
		
		
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

	

</style>
