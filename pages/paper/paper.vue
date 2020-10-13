<template>
	<view class="body">
		<block v-for="(item,index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		
	</view>
</template>

<script>
	import paperList from '@/components/paper/paper-list.vue'
	
	export default {
		components:{
			paperList
		},
		data() {
			return {
				list:[
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"20:45",
						data:"描述信息",
						noreadnum:2
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"20:45",
						data:"描述信息",
						noreadnum:0
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"20:45",
						data:"描述信息",
						noreadnum:2
					},
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped lang="scss">
	.body{
		padding: 0rpx 20rpx;
	}
	
</style>
