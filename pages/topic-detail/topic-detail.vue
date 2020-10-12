<!-- 话题详情页面 -->
<template>
	<view>
		<topic-info :info="info"></topic-info>
		<divider></divider>
		<view class="recommend-item" hover-class="bg-light" v-for="(item,index) in hotList" :key="index" >
			<text class="iconfont icon-dizhi"></text>
			<text class="text">
				{{item.title}}
			</text>
		</view>
		<divider></divider>
		
		<!-- tab标签 -->
		<view class="tab">
			<view class="tab-item" v-for="(item,index) in tabBars" :key="index" 
			 :class="index==tabindex?'active':''" @click="changeTab(index)">{{item.name}}</view>
		</view>
		
		<template v-if="listData.length > 0">
			<block v-for="(item,index) in listData" :key="index">
				<common-list :item="item" :index="index" ></common-list>
				<divider></divider>
			</block>
		</template>
		<template v-else>
			<view class="position-relative" style="height: 2px;">
				<no-thing></no-thing>
			</view>
		</template>
		
		<!-- 上拉加载 -->
		<load-more :loadText="loadText"></load-more>
		
		
	</view>
</template>

<script>
	
	import topicInfo from '@/components/topic-detail/topic-info.vue';
	import commonList from '@/components/common/common-list.vue';
	import noThing from '@/components/common/no-thing.vue';
	import loadMore from '@/components/common/load-more.vue';
	
	
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
			topicInfo,
			commonList,
			noThing,
			loadMore
		},
		data() {
			return {
				info:{
						title: "淘宝记录簿",
						titlepic: "../../static/demo/topicpic/13.jpeg",
						desc: "120斤到85斤 我的反转人生",
						totalnum: 20,
						todaynum: 15
					},
				hotList:[
					{
						title:"[新人必读] uniapp哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈"
					},
					{
						title:"[新人必读] uniapp哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈"
					}
				],
				list1:[],
				loadText1:"上拉加载更多",
				list2:[],
				loadText2:"上拉加载更多",
				tabindex:0,
				tabBars:[
					{
						name:"默认"
					},
					{
						name:"最新"
					}
				]
			}
		},
		onLoad(e) {
			if(e.detail){
				let res = JSON.stringify(e.detail);
				console.log(res);
			}
			
			//添加数据
			for (var i = 0; i < 10; i++) {
				this.list1.push(itemObj);
			}
			
			//this.list2.push(itemObj);
			
		},
		//页面滚动触底事件
		onReachBottom() {
			console.log("上拉加载");
			this.loadMore();
		},
		methods: {
			changeTab(index){
				this.tabindex = index;
			},
			//加载更多
			loadMore(){
				//记录当前位置
				let index = this.tabindex;
				//判断状态
				if(this.loadText != '上拉加载更多'){
					return;
				}
				
				//设置为加载状态
				this['loadText'+(index+1)] = '加载中..';
				//加载数据
				setTimeout(()=>{
					this['list'+(index+1)] = this['list'+(index+1)].concat([itemObj]);
					//改回状态
					this['loadText'+(index+1)] = '上拉加载更多';
				},2000);
				
				
			}
		},
		computed: {
			listData() {
				if(this.tabindex == 0){
					return this.list1;
				}else{
					return this.list2;
				}
			},
			loadText(){
				if(this.tabindex == 0){
					return this.loadText1;
				}else{
					return this.loadText2;
				}
			}
		},
	}
</script>

<style lang="scss">

	.recommend-item{
		padding: 10rpx 20rpx;
		display: flex;
		align-items: center;
		border-bottom: 1rpx solid #F7F7F7;
		.text{
			font-size: medium;
			padding-left: 10rpx;
			overflow: hidden;
			text-overflow: ellipsis;
			white-space: nowrap;
		}
	}
	
	.bg-light{
		background-color: #F7F7F7;
	}
	
	/**
	 * tab样式
	 */
	.tab{
		display: flex;
		align-items: center;
		padding: 15rpx 0rpx;
		border-bottom: 1px solid #F7F7F7;
		.tab-item{
			flex: 1;
			font-size: 30rpx;
			display: flex;
			justify-content: center;
			align-items: center;
		}
		
		.tab-item.active{
			color: #09BB07;
			font-weight: bold;
		}
	}

</style>
