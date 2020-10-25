<!-- 好友列表 -->
<template>
	<view class="body">
		<!-- 顶部选项卡 -->
		<swiper-tab-head :tabbars="tabbars" :tabIndex="tabIndex" @tabClick="tabClick" :scrollItemStyle="'width:33%'"></swiper-tab-head>
		<!-- 好友列表 -->
		<!-- <block v-for="(item,index) in list" :key="index">
			<user-list :item="item" :index="index"></user-list>
		</block> -->
		<view class="uni-tab-bar">
			<!-- 横向滚动 -->
			<swiper class="swiper-box" v-bind:style="{height:scrollHeight+'px'}" :current="tabIndex" @change="swiperChange">
				<block v-for="(items,index) in newsList" :key="index">
					<swiper-item>
						<!-- scroll-view 需要设置高度才可以 设置为父容器的100%  -->
						<scroll-view scroll-y class="list" v-on:scrolltolower="loadMore(index)">
							 <template v-if="items.list.length>0">
								<!-- 纵向滚动 -->
									<block v-for="(item,itemIndex) in items.list" :key="itemIndex">
										<!-- 小条目 -->
										<user-list :item="item" :index="itemIndex"></user-list>
									</block>
									<!-- 上拉加载 -->
									<load-more v-bind:loadText="items.loadText"></load-more>
							</template>
							 <template v-else>
								<no-thing></no-thing>
							</template>
						</scroll-view>
					</swiper-item>
				</block>
			</swiper>
		</view>
	</view>
</template>

<script>
	import swiperTabHead from '@/components/index/swiper-tab-head.vue';
	import userList from '@/components/common/user-list.vue';
	import loadMore from "../../components/common/load-more.vue";
	import noThing from "../../components/common/no-thing.vue";

	let itemObj = {
		userpic: "../../static/demo/userpic/2.jpg",
		username: "昵称",
		age: 20,
		sex: 0,
		isguanzhu: false
	};

	export default {
		components: {
			swiperTabHead,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				tabbars: [{
						name: "互关",
						id: "huguan",
						num: 3
					},
					{
						name: "关注",
						id: "guanzhu",
						num: 3
					},
					{
						name: "粉丝",
						id: "fensi",
						num: 10
					}
				],
				tabIndex: 0,
				scrollHeight:700,
				newsList:[
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					}
				]
			}
		},
		methods: {
			tabClick(index) {
				this.tabIndex = index;
			},
			swiperChange(event){
				let currentIndex = event.detail.current;
				this.tabIndex = currentIndex;
			},
			loadMore(index){
				//判断状态
				if (this.newsList[index].loadText != "上拉加载更多···") {
					return;
				}
				//模拟获取到了数据
				this.newsList[index].loadText = "加载中···";
				setTimeout(() => {
					this.newsList[index].list.push(itemObj);
					//还原状态
					this.newsList[index].loadText = "上拉加载更多···";
				}, 1000);
				//this.newsList[index].loadText = "没有更多数据了";
			}
		},
		//导航栏点击事件
		onNavigationBarButtonTap(e) {
			switch (0) {
				case 0:
					//关闭界面
					uni.navigateBack({
						delta: 1
					});
					break;
				default:
					break;
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight;
					//可视区域高度减去顶部标题栏高度
					this.scrollHeight = height - uni.upx2px(100);
				}
			})
		}
	}
</script>

<style lang="scss">
	.body {
		padding: 0 20rpx;
		
		// .list{
		// 	height: 100%;
		// }
	}

	
</style>
