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
		<upload-images @upload-img="uploadImages"></upload-images>
		<!-- 弹出的提示框 -->
		<uni-popup :show="showPopup"  position="middle" mode="fixed" @hidePopup="togglePopup()">
			<!-- 显示自己的内容 -->
			<view class="popup-content">
				<view class="popup-content-img">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view class="text">
					1.涉及黄色,政治,广告及骚扰信息
				</view>
				<view class="text">
					2.涉及人身攻击
				</view>
				<view class="text">
					3.留联系方式,透露他人隐私
				</view>
				<view class="text">
					一经核实将被封禁,情节严重者永久封禁
				</view>
				<button type="default" @tap="togglePopup()">朕知道了</button>
			</view>
		</uni-popup>
		
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	import uploadImages from "../../components/common/upload-images.vue";
	//使用官方的弹出框组件
	import uniPopup from "../../components/uni-popup/uni-popup.vue";
	//定义选项
	let privacys = ["所有人可见","仅自己可见"];

	export default {
		components:{
			uniNavBar,
			uploadImages,
			uniPopup
		},
		data() {
			return {
				isShowSaveData:false,//记录是否已经显示了保存草稿提示框  
				showPopup:true,
				privacy:privacys[0],
				text:"",
				imageList:[]
			}
		},
		onBackPress() {	//返回事件
			if(this.isShowSaveData){
				return;
			}
			//判断是否输入了数据
			if (!this.text && this.imageList.length == 0) {
				return;
			}
			this.saveData();
			return true;
		},
		methods: {
			saveData(){
				//弹出提示框
				uni.showModal({
					title: '提示',
					content: '是否保存为草稿?',
					showCancel: true,
					cancelText: '否',
					confirmText: '是',
					success: res => {
						//判断点击的是什么按钮
						if (res.confirm) {
							console.log("已保存为草稿");
						} else{
							console.log("取消保存为草稿");
						}
						this.isShowSaveData = true;
						//返回到上一页
						uni.navigateBack({	//这个方法还会调用到 onBackPress方法中
							delta: 1
						});
					}
				});
			},
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
			},
			uploadImages(arr){
				console.log(JSON.stringify(arr));
				this.imageList = arr;
				console.log(this.imageList);
			},
			togglePopup(){	//关闭弹出框
				this.showPopup = false;
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
	
	/**
	 * 弹出框中图片的样式
	 */
	.popup-content{
		width: 500upx;
	}
	.popup-content .popup-content-img{
		display: flex;
		justify-content: center;
		align-items: center;
		margin-bottom: 20upx;
	}
	.popup-content .popup-content-img image{
		width: 70%;
	}
	
	.popup-content button{
		margin-top: 20upx;
		background-color: #FEE42A;
		color: #171606;
	}
</style>
