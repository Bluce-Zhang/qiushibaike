<!-- 顶部滚动导航栏组件 -->
<template>
	<view class="uni-tab-bar">
		<scroll-view class="uni-swiper-tab" scroll-x>
			<block v-for="(item,index) in tabbars" v-bind:key="index">
				<view class="swiper-tab-list" v-bind:class="{'active':(index==tabIndex)}" v-on:click="tabClick(index)">
					{{item.name}}
					<view class="swiper-tab-bottom"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props:{
			tabbars:Array,
			tabIndex:Number
		},
		methods:{
			tabClick(index){
				//给父组件传值
				this.$emit('tabClick',index);
			}
		}
	}
</script>

<style scoped>
	.uni-swiper-tab{
		border-bottom: 1px solid #EEEEEE;
	}
	
	.swiper-tab-list{
		color: #969696;
		font-weight: bold;
	}
	
	.uni-tab-bar .active {
		color: #343434;
	}
	
	.uni-swiper-tab .active .swiper-tab-bottom{
		height: 10rpx;
		background-color: #FEDE33;
		margin: 0rpx 25rpx;
		border-radius: 5rpx;
	}
</style>
