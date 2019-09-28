	<!-- 动态页面tab子组件 -->
<template>
	<view>
		<!-- 上部导航 -->
		<uni-nav-bar :fixed="true" :border="false" @click-left="signIn()" @click-right="toPublish()">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao">
						
					</view>
				</view>
			</block>
			<!-- 中间 -->
			<block>
				<view class="nav-middle">
					<block v-for="(tabBar,index) in tabBars" v-bind:key="tabBar.id">
						<view v-bind:class="{'active':index==tabIndex}" @tap="changeTab(index)">
							{{tabBar.name}}
							<view v-if="(index==tabIndex)" class="nav-middle-line"></view>
						</view>
					</block>
				</view>
			</block>
			<!-- 右边 -->
			<block slot="right">
				<view class="nav-right">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue';
	export default {
		components:{
			uniNavBar
		},
		props:{
			tabBars:Array,
			tabIndex:Number
		},
		data() {
			return {
				
			}
		},
		methods:{
			changeTab(index){
				//给父页面发送事件
				this.$emit("change-tab",index);
			},
			signIn(){
				
			},
			toPublish(){
				//跳转到发布页面
				uni.navigateTo({
					url:"../publish/publish"
				});
			}
		}
	}
</script>

<style scoped>
	/* 顶部导航样式 */
	.nav-left>view,.nav-right>view{
		font-size: 40rpx;
	}
	.nav-left>view{
		color: #FF9619;
	}
	.nav-left{
		display: flex;
		align-items: center;
		margin-left: 30rpx;
	}
	.nav-right{
		display: flex;
		width: 100%;
		justify-content: center;
		align-items: center;
	}
	.nav-middle{
		margin-left: -45rpx;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.nav-middle view{
		padding: 0rpx 15rpx;
		font-size: 35rpx;
		color: #969696;
		font-weight: bold;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	.nav-middle .active{
		color: #171606 !important;
	}
	/**
	 * 指示线的样式
	 */
	.nav-middle-line{
		border: 6rpx solid #FEDE33;
		border-radius: 10rpx;
		width: 20%;
		margin-top: -8rpx;
	}
</style>
