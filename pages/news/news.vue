<!-- 动态页面 -->
<template>
	<view>
		<!-- 顶部导航栏 -->
		<news-nav-bar :tabBars="tabBars" :tabIndex="tabIndex" @change-tab="changeTab"></news-nav-bar>
		<!-- 列表 -->
		<view class="uni-tab-bar">
			<!-- 横向滚动 -->
			<swiper class="swiper-box" v-bind:style="{height:scrollHeight+'px'}" :current="tabIndex" @change="swiperChange">
				<!-- 关注子页面 -->
				<swiper-item>
					<scroll-view scroll-y class="list" v-on:scrolltolower="loadMore()">
						<template v-if="guanzhu.list.length>0">
						 <block v-for="(item,index) in guanzhu.list" :key="index">
						 	<common-list :item="item" :index="index"></common-list>
						 </block>
						 <!-- 上拉加载 -->
						 <load-more v-bind:loadText="guanzhu.loadText"></load-more>
						 </template>
						 <template v-else>
							 <no-thing></no-thing>
						 </template>
					</scroll-view>
				</swiper-item>
				<!-- 话题子页面 -->
				<swiper-item>
					<scroll-view scroll-y class="list">
						<!-- 搜索输入框 -->
						<view class="search-input">
							<input type="text" placeholder-class="icon iconfont icon-sousuo search-input-placeholder" placeholder="请输入搜索内容" />
						</view>
						<!-- 轮播图组件 -->
						<view class="tipic-swiper animated bounceInDown">
							<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
								<block v-for="(item,index) in topic.swiper" :key="index">
									<swiper-item>
										<view class="swiper-item">
											<image :src="item.src" mode="widthFix" lazy-load></image>
										</view>
									</swiper-item>
								</block>
							</swiper>
						</view>
						<!-- 热门分类 -->
						<topic-nav :nav="topic.nav"></topic-nav>
						<!-- 最近更新列表 -->
						<view class="topic-list">
							<view>
								最近更新
							</view>
							<block v-for="(item,index) in topic.list" :key="index">
								<topic-list-item :item="item"></topic-list-item>
							</block>
						</view>
						
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
	</view>
</template>

<script>
	import newsNavBar from '../../components/news/news-nav-bar.vue';
	import commonList from "../../components/common/common-list.vue";
	import loadMore from "../../components/common/load-more.vue";
	import noThing from "../../components/common/no-thing.vue";
	import topicNav from "../../components/news/topic-nav.vue";
	import topicListItem from '../../components/news/topic-list-item.vue';
	let itemObj = {
		userpic:"../../static/demo/userpic/8.jpg",
		username:"三鱼先生",
		sex:0,
		age:25,
		isguanzhu:false,
		title:"六道快手家常菜,好吃又下饭,家人都喜欢,哈哈哈哈哈哈哈哈",
		titlepic:"../../static/demo/datapic/16.jpg",
		video:false,
		share:false,
		path:"深圳 龙岗",
		sharenum:20,
		commentnum:30,
		goodnum:20
	};
	export default {
		components: {
			newsNavBar,
			commonList,
			loadMore,
			noThing,
			topicNav,
			topicListItem
		},
		data() {
			return {
				scrollHeight:700,//滚动区域的高度
				tabIndex:0,
				tabBars:[
					{name:"关注",id:0},
					{name:"话题",id:1}
				],
				guanzhu:{
					loadText:"上拉加载更多···",
					list:[
						//文字条目
						{
							userpic:"../../static/demo/userpic/8.jpg",
							username:"三鱼先生",
							sex:0,
							age:25,
							isguanzhu:false,
							title:"六道快手家常菜,好吃又下饭,家人都喜欢,哈哈哈哈哈哈哈哈",
							titlepic:"",
							video:false,
							share:false,
							path:"深圳 龙岗",
							sharenum:20,
							commentnum:30,
							goodnum:20
						},
						//图文条目
						{
							userpic:"../../static/demo/userpic/8.jpg",
							username:"三鱼先生",
							sex:0,
							age:25,
							isguanzhu:false,
							title:"六道快手家常菜,好吃又下饭,家人都喜欢,哈哈哈哈哈哈哈哈",
							titlepic:"../../static/demo/datapic/16.jpg",
							video:false,
							share:false,
							path:"深圳 龙岗",
							sharenum:20,
							commentnum:30,
							goodnum:20
						},
						//视频条目
						{
							userpic:"../../static/demo/userpic/8.jpg",
							username:"三鱼先生",
							sex:0,
							age:25,
							isguanzhu:false,
							title:"六道快手家常菜,好吃又下饭,家人都喜欢,哈哈哈哈哈哈哈哈",
							titlepic:"../../static/demo/datapic/16.jpg",
							video:{
								looknum:"25w",
								long:"2:24"
							},
							share:false,
							path:"深圳 龙岗",
							sharenum:20,
							commentnum:30,
							goodnum:20
						},
						//分享条目
						{
							userpic:"../../static/demo/userpic/8.jpg",
							username:"三鱼先生",
							sex:0,
							age:25,
							isguanzhu:false,
							title:"六道快手家常菜,好吃又下饭,家人都喜欢,哈哈哈哈哈哈哈哈",
							titlepic:"",
							video:false,
							share:{
								title:"分享的标题",
								titlepic:"../../static/demo/datapic/10.jpg"
							},
							path:"深圳 龙岗",
							sharenum:20,
							commentnum:30,
							goodnum:20
						}
					]
				},
				topic:{
					swiper:[	//轮播图
						{
							src:"../../static/demo/datapic/16.jpg"
						},
						{
							src:"../../static/demo/datapic/16.jpg"
						},
						{
							src:"../../static/demo/datapic/16.jpg"
						}
					],
					nav:[
						{name:"最新"},
						{name:"游戏"},
						{name:"情感"},
						{name:"打卡"},
						{name:"故事"},
						{name:"喜爱"}
					],
					list:[
						{
							title:"淘宝记录簿",
							titlepic:"../../static/demo/topicpic/13.jpeg",
							desc:"120斤到85斤 我的反转人生",
							totalnum:20,
							todaynum:15
						},
						{
							title:"淘宝记录簿",
							titlepic:"../../static/demo/topicpic/13.jpeg",
							desc:"120斤到85斤 我的反转人生",
							totalnum:20,
							todaynum:15
						},
						{
							title:"淘宝记录簿",
							titlepic:"../../static/demo/topicpic/13.jpeg",
							desc:"120斤到85斤 我的反转人生",
							totalnum:20,
							todaynum:15
						}
					]
				}
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
		methods: {
			changeTab(index){
				this.tabIndex = index;
				console.log("切换条目:"+index);
			},
			swiperChange(event){
				let currentIndex = event.detail.current;
				this.tabIndex = currentIndex;
			},
			loadMore(){
				//判断状态
				if (this.guanzhu.loadText != "上拉加载更多···") {
					return;
				}
				//模拟获取到了数据
				this.guanzhu.loadText = "加载中···";
				setTimeout(() => {
					this.guanzhu.list.push(itemObj);
					//还原状态
					this.guanzhu.loadText = "上拉加载更多···";
				}, 1000);
				//this.guanzhu.loadText = "没有更多数据了";
			}
		}
	}
</script>

<style>
	/**
	 * 搜索框样式
	 */
	.search-input{
		padding: 20rpx;
	}
	
	.search-input>input{
		padding: 20rpx 15rpx;
		border-radius: 15rpx;
		background-color: #F4F4F4;
	}
	
	.search-input-placeholder{
		text-align: center;
	}
	
	/**
	 * 轮播组图样式
	 */
	.tipic-swiper{
		padding: 0rpx 20rpx 20rpx 20rpx;
	}
	
	.swiper-item image{
		width: 100%;
		border-radius: 20rpx;
	}
	
	/**
	 * 最新更新列表样式
	 */
	.topic-list{
		padding: 20rpx 20rpx;
	}
	.topic-list>view:first-child{
		margin-bottom: 40rpx;
	}

</style>
