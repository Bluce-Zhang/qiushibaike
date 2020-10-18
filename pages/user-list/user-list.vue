<template>
	<view>
		<!-- 顶部选项卡 -->
		<swiper-tab-head :tabbars="tabbars" 
			:tabIndex="tabIndex" 
			@tabClick="tabClick"
			 :scrollItemStyle="'width:33%'"
			 ></swiper-tab-head>
		好友列表
	</view>
</template>

<script>
	import swiperTabHead from '@/components/index/swiper-tab-head.vue';
	export default {
		components:{
			swiperTabHead
		},
		data() {
			return {
				tabbars:[
					{name:"互关",id:"huguan",num:3},
					{name:"关注",id:"guanzhu",num:3},
					{name:"粉丝",id:"fensi",num:10}
				],
				tabIndex:0,
			}
		},
		methods: {
			tabClick(index){
				this.tabIndex = index;
			}
		},
		//导航栏点击事件
		onNavigationBarButtonTap(e) {
			switch (0){
				case 0:
				//关闭界面
				uni.navigateBack({
					delta:1
				});
					break;
				default:
					break;
			}
		}
	}
</script>

<style>

</style>
