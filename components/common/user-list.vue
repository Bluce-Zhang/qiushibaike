<!-- 好友列表条目 -->
<template>
	<view>
		<view class="common-flex-align-items user-list animated fadeInLeft fast">
			<image class="head" :src="item.userpic" mode="widthFix"></image>
			<view class="middle">
				<view class="name">{{item.username}}</view>
				<tag-sex-age class="sex-tag" :sex="item.sex" :age="item.age"></tag-sex-age>
			</view>
			<view v-if="item.isguanzhu" class="icon iconfont icon-xuanze-yixuan select"></view>
			<view v-else class="icon iconfont icon-zengjia1 add"></view>
		</view>
	</view>
</template>

<script>
	import tagSexAge from '@/components/common/tag-sex-age.vue';
	export default {
		components:{
			tagSexAge
		},
		props:{
			item:Object,
			index:Number
		}
	}
	
</script>

<style scoped lang="scss">
	.user-list {
		padding: 11rpx 15rpx;
		border-bottom: 1rpx solid #CCCCCC;
	
		.head {
			height: 100rpx;
			width: 100rpx;
			border-radius: 50%;
			flex-shrink: 0;
			margin-right: 20rpx;
		}
	
		.middle {
			flex: 1;
			padding: 0rpx 11rpx;
	
			.name {
				font-size: 35rpx;
			}
	
			.sex-tag {
				display: inline-block;
			}
		}
	
		.select {
			width: 80rpx;
			color: #CCCCCC;
			text-align: center;
		}
	
		.add {
			width: 80rpx;
			color: #F8791B;
			text-align: center;
		}
	}
</style>
