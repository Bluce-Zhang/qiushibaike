<template>
	<!-- 小纸条列表 -->
	<view class="paper-list animated fadeInLeft fast">
		<!-- 头像 -->
		<image class="head-image" mode="widthFix" :src="item.userpic" lazy-load></image>
		<view class="content">
			<view class="name">
				{{item.username}}
				<view class="time">{{item.time}}</view>
			</view>
			<view class="info">
				<view>{{item.data}}</view>
				<template v-if="item.noreadnum>0">
					<uni-badge text="1" type="error" @click="badgeClick()"></uni-badge>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '@/components/uni-badge/uni-badge.vue'; //引入角标组件
	
	export default{
		components:{
			uniBadge
		},
		props:{
			item:Object,
			index:Number
		},
		methods:{
			badgeClick(){
				console.log("角标点击事件");
			}
		}
	}
	
</script>

<style scoped lang="scss">
	.paper-list{
		display: flex;
		border-bottom: 1rpx solid #EEEEEE;
		padding: 20rpx 0rpx;
		.head-image{
			width: 100rpx;
			height: 100rpx;
			border-radius: 100%;
			margin-right: 20rpx;
			flex-shrink: 0;
		}
		
		.content{
			flex: 1;
			
			.name{
				display: flex;
				justify-content: space-between;
				align-items: center;
				font-size: 35rpx;
				// font-weight: bold;
				
				.time{
					font-weight: normal;
					font-size: 30rpx;
					color: #CBCBCB;
				}
			}
			
			.info{
				display: flex;
				justify-content: space-between;
				align-items: center;
				view{
					color: #888888;
				}
			}
			
		}
	}
</style>
