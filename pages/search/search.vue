<template>
	<view>
		搜索页
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onNavigationBarButtonTap(e) {	//导航栏按钮的点击事件
			if (e.index == 0) {	//取消按钮  关闭界面
				uni.navigateBack({
					delta:1
				})
			}
		},
		onNavigationBarSearchInputChanged(e) {	//导航栏搜索框输入事件
			console.log("输入"+e.text);
		},
		onNavigationBarSearchInputConfirmed(e) {		//软键盘上的搜索按钮点击事件
			console.log("搜索"+e.text);
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
