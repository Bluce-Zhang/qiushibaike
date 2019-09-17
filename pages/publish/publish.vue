<template>
	<view>
		<!--标题栏  使用uniapp 官方的自定义标题栏-->
		<uni-nav-bar v-bind:statusBar="true" left-icon="back" rightText="发布" @click-left="back" @click-right="submit" >
			<view class="nav-title-select" @tap="changeLook">
				{{privacy}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!--输入框-->
		<view class="uni-textarea">
			<textarea v-model="text" placeholder="请说一句话吧~" />
		</view>
		<!--图片选择-->
		
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	//定义选项
	let privacys = ["所有人可见","仅自己可见"];
	export default {
		components:{
			uniNavBar
		},
		data() {
			return {
				privacy:privacys[0],
				text:""
			}
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				});
			},
			submit(){
				console.log("发布");
			},
			changeLook(){
				console.log("改变隐私");
				uni.showActionSheet({
					itemList:privacys,
					success: (res) => {
						this.privacy = privacys[res.tapIndex];
					}
				});
			}
		}
	}
</script>

<style>
	.nav-title-select{
		display: flex;
		height: 100%;
		justify-content: center;
		align-items: center;
	}
	.uni-textarea{
		border-bottom: 1px solid #EEEEEE;
	}
</style>
