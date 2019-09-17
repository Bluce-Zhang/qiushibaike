<template>
	<view>
		<!-- 顶部选项卡 -->
		<swiper-tab-head :tabbars="tabbars" :tabIndex="tabIndex" @tabClick="tabClick"></swiper-tab-head>
		
		<view class="uni-tab-bar">
			<!-- 横向滚动 -->
			<swiper class="swiper-box" v-bind:style="{height:scrollHeight+'px'}" :current="tabIndex" @change="swiperChange">
				<block v-for="(items,index) in newsList" :key="index">
					<swiper-item>
						<scroll-view scroll-y class="list" v-on:scrolltolower="loadMore(index)">
							 <template v-if="items.list.length>0">
								<!-- 纵向滚动 -->
									<block v-for="(item,itemIndex) in items.list" :key="itemIndex">
										<!-- 小条目 -->
										<index-list v-bind:item="item" v-bind:index="itemIndex"></index-list>
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
	// 引入子组件
	import swiperTabHead from "../../components/index/swiper-tab-head.vue";
	import indexList from "../../components/index/index-list.vue";
	import loadMore from "../../components/common/load-more.vue";
	import noThing from "../../components/common/no-thing.vue";
	
	let itemObj = {
							userpic:"../../static/demo/userpic/12.jpg",
							username:"昵称",
							isguanzhu:false,
							title:"标题",
							type:"img",//img 图文 video 视频
							titlepic:"../../static/demo/banner1.jpg",
							playnum:200000,
							long:"2:47",
							infonum:{
								index:0, //0:没有顶,没有踩 1:顶  2:踩
								dingnum:8,
								cainum:8
							},
							commentnum:10,
							sharenum:10
						};
	
	export default {
		components:{
			swiperTabHead,
			indexList,
			loadMore,
			noThing
		},
		data() {
			return {
				scrollHeight:700,//滚动区域的高度
				tabIndex:0,//默认选中的位置
				tabbars:[
					{name:"关注",id:"guanzhu"},
					{name:"推荐",id:"tuijian"},
					{name:"体育",id:"tiyu"},
					{name:"热点",id:"redian"},
					{name:"财经",id:"caijing"},
					{name:"娱乐",id:"yule"},
					{name:"军事",id:"junshi"},
					{name:"历史",id:"lishi"},
					{name:"本地",id:"bendi"}
				],
				newsList:[
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					},
					{
						loadText:"上拉加载更多···",
						list:[itemObj,itemObj,itemObj]
					}
				],
				list:[
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:false,
						title:"标题",
						type:"img",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:1, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:true,
						title:"标题",
						type:"video",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:2, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						isguanzhu:true,
						title:"标题",
						type:"video",//img 图文 video 视频
						titlepic:"../../static/demo/banner1.jpg",
						playnum:200000,
						long:"2:47",
						infonum:{
							index:0, //0:没有顶,没有踩 1:顶  2:踩
							dingnum:10,
							cainum:10
						},
						commentnum:10,
						sharenum:10
					}
				]
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
		},
		onNavigationBarSearchInputClicked() {
			//跳转到搜索页面
			uni.navigateTo({
				url:"../search/search"
			});
		},
		onNavigationBarButtonTap(e) {	//标题栏上的按钮的点击事件
			switch (e.index){
				case 0:	//签到事件
				
					break;
				case 1:	//发表按钮  跳转到发表界面
					uni.navigateTo({
						url:"../publish/publish"
					});
					break;
			}
		},
		methods: {
			tabClick(index){
				//修改选中的位置
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
		}
	}
</script>

<style>

</style>
