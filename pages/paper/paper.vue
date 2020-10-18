<template>
	<view class="body">
		<!-- 菜单 -->
		<paper-left-popup :show="show" @hide="hidePopup()" @addFriend="addFriend()" @clear="clear()"></paper-left-popup>
		<!-- 小纸条列表 -->
		<block v-for="(item,index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		<!-- 加载更多 -->
		<load-more :loadText="loadMoreText"></load-more>
	</view>
</template>

<script>
	import paperList from '@/components/paper/paper-list.vue';
	import loadMore from '@/components/common/load-more.vue';
	import paperLeftPopup from '@/components/paper/paper-left-popup.vue'
	
	import objectUtil from '@/common/js/objectUtil.js';
	
	export default {
		components:{
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				show:false,
				list:[],
				loadMoreText:"上拉加载更多"
			}
		},
		methods: {
			getData(){
				//1.从服务器请求数据
				//2.给数组赋值
				//3.结束下拉刷新
				let obj = {
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"20:45",
						data:"描述信息",
						noreadnum:2
					};
				let arr = [];
				for (var i = 0; i < 10; i++) {
					var newObj = objectUtil.deepCopy(obj);
					newObj.username = "昵称"+i;
					arr.push(newObj);
				}
				
				this.list = arr;
				
				uni.stopPullDownRefresh();
				
			},
			loadMore(){
				//加载更多
				if(this.loadMoreText != '上拉加载更多'){return;}
				this.loadMoreText = '正在加载中..';
				setTimeout(()=>{
					let obj = {
							userpic:"../../static/demo/userpic/12.jpg",
							username:"昵称",
							time:"20:45",
							data:"描述信息",
							noreadnum:2
						};
					this.list.push(obj);
					this.loadMoreText = '上拉加载更多';
				},1000);
			},
			addFriend(){
				console.log("添加好友");
				//同时隐藏弹窗
				this.hidePopup();
			},
			clear(){
				console.log("清除缓存");
				//同时隐藏弹窗
				this.hidePopup();
			},
			hidePopup(){
				this.show = false;
			},
			showPopup(){
				this.show = true;
			}
		},
		onLoad() {
			setTimeout(()=>{
				uni.startPullDownRefresh();
			},500);
		},
		onPullDownRefresh() {
			console.log("下拉刷新");
			setTimeout(()=>{
				this.getData();
			},2000);
			
		},
		onReachBottom() {
			this.loadMore();
		},
		onNavigationBarButtonTap(e) {
			//console.log(JSON.stringify(e));
			switch (e.index){
				case 0:
				console.log("点击的左边按钮");
				//跳转到好友列表页面
				uni.navigateTo({
					url:'../user-list/user-list'
				})
				this.hidePopup();
					break;
				case 1:
				console.log("点击的右边按钮");
					this.showPopup();
					break;
				default:
					break;
			}
		}
	}
</script>

<style scoped lang="scss">
	.body{
		padding: 0rpx 20rpx;
	}

</style>
