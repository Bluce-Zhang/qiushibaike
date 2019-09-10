<!-- 列表条目组件 -->
<template>
	<view class="index-list animated bounceIn">
		<!--第一行 头像 昵称 关注-->
		<view class="index-list1">
			<view>
				<image v-bind:src="item.userpic" mode="widthFix" lazy-load></image>
				{{item.username}}
			</view>
			<template v-if="item.isguanzhu">
				<view  v-on:tap="guanzhu(item.isguanzhu)">已关注</view>
			</template>
			<template v-else>
				<view v-on:tap="guanzhu(item.isguanzhu)">+关注</view>
			</template>
		</view>
		<!--第二行标题-->
		<view class="index-list2" v-on:click="toDetail()">
			{{item.title}}
		</view>
		<!--第三行 大图-->
		<view class="index-list3 uni-flex" v-on:click="toDetail()">
			<!--图片-->
			<image v-bind:src="item.titlepic" mode="widthFix" lazy-load></image>
			<!-- 视频 -->
			<template v-if="item.type == 'video'">
				<view class="index-list-play icon iconfont icon-bofang"></view>
				<view class="index-list-play-info">{{item.playnum}}次播放 {{item.long}}</view>
			</template>

		</view>
		<!--第四行 赞 踩 评论 转发 -->
		<view class="index-list4">
			<view>
				<!-- 赞 -->
				<view v-bind:class="{'active':(item.infonum.index == 1)}">
					<view class="icon iconfont icon-icon_xiaolian-mian" v-on:tap="caoZuo('ding')"></view>
					<view>{{item.infonum.dingnum}}</view>
				</view>
				<!-- 踩 -->
				<view v-bind:class="{'active':(item.infonum.index == 2)}">
					<view class="icon iconfont icon-kulian" v-on:tap="caoZuo('cai')"></view>
					<view>{{item.infonum.cainum}}</view>
				</view>
			</view>
			<view>
				<!-- 评论 -->
				<view>
					<view class="icon iconfont icon-pinglun1"></view>
					<view>{{item.commentnum}}</view>
				</view>
				<!-- 转发 -->
				<view>
					<view class="icon iconfont icon-zhuanfa"></view>
					<view>{{item.sharenum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods:{
			guanzhu(isguanzhu){
				if(isguanzhu){
					uni.showToast({
						title:"取消关注"
					});
				}else{
					uni.showToast({
						title:"关注成功"
					});
				}
				//改变状态
				this.item.isguanzhu = !this.item.isguanzhu;
			},
			caoZuo(type){
				switch (type){
					case 'ding':	//顶事件
						if (this.item.infonum.index == 1) {return;}
						//加上顶的个数
						this.item.infonum.dingnum++;
						if (this.item.infonum.index == 2) {
							//减去踩的个数
							this.item.infonum.cainum--;
						}
						//修改状态为ding
						this.item.infonum.index = 1;
						break;
					case 'cai':		//踩事件
						if(this.item.infonum.index == 2){return;}
						//加上踩的个数
						this.item.infonum.cainum++;
						if (this.item.infonum.index == 1) {
							//减去顶的个数
							this.item.infonum.dingnum--;
						}
						//修改状态为踩
						this.item.infonum.index = 2;
						break;
				}
			},
			toDetail(){
				console.log("跳转到详情页");
			}
			
		}
	}
</script>
<!-- scoped 代表只能当前组件使用 -->
<style scoped>
	.index-list {
		padding: 30rpx 20rpx;
		border-bottom: 2rpx solid #EFEFEF;
	}

	.index-list1 {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.index-list1>view:first-child {
		display: flex;
		justify-content: center;
		align-items: center;
		color: #999999;
	}

	.index-list1>view:first-child image {
		width: 80rpx;
		height: 80rpx !important;
		border-radius: 100%;
		margin-right: 20rpx;
	}

	.index-list1>view:last-child {
		display: flex;
		align-items: center;
		background-color: #F4F4F4;
		border-radius: 10rpx;
		padding: 4rpx 10rpx;
	}

	.index-list2 {
		padding: 20rpx 10rpx;
		font-size: 35rpx;
	}

	.index-list3 {
		position: relative;
		justify-content: center;
		align-items: center;
	}

	.index-list3>image {
		width: 100%;
		border-radius: 20rpx;
	}

	.index-list3>.index-list-play {
		position: absolute;
		font-size: 130rpx;
		color: #FFFFFF;
	}

	.index-list3>.index-list-play-info {
		position: absolute;
		background-color: rgba(51, 51, 51, 0.72);
		color: #FFFFFF;
		font-size: 15rpx;
		bottom: 10rpx;
		right: 20rpx;
		border-radius: 20rpx;
		padding: 0 15rpx;
	}

	.index-list4 {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 20rpx 0 10rpx 0;
	}

	.index-list4 view {
		color: #CCCCCC;
	}

	.index-list4>view:first-child {
		display: flex;
		align-items: center;
	}

	.index-list4>view:last-child {
		display: flex;
		align-items: center;
	}

	.index-list4>view>view {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.index-list4>view>view>view {
		margin-left: 15rpx;
	}

	.index-list4 .active view {
		color: #FEE42A;
	}
</style>
