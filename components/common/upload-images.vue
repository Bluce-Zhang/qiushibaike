	<!-- 上传图片组件 -->
<template>
	<view class="uni-list list-pd">
		<view class="uni-list-cell cell-pd">
			<view class="uni-uploader">
				<view class="uni-uploader-head">
					<view class="uni-uploader-title">点击可预览选好的图片</view>
					<view class="uni-uploader-info">{{imageList.length}}/9</view>
				</view>
				<view class="uni-uploader-body">
					<view class="uni-uploader__files">
						<block v-for="(image,index) in imageList" :key="index">
							<view class="uni-uploader__file">
								<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
								<!--删除按钮-->
								<view class="icon iconfont icon-shanchu img-delete" @tap="deleteImage(index)"></view>
							</view>
						</block>
						<view class="uni-uploader__input-box">
							<view class="uni-uploader__input" @tap="chooseImage"></view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	];
	var sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	];
	export default {
		data() {
			return {
				imageList: [],
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9]
			}
		},
		methods:{
			chooseImage: async function() {
				if (this.imageList.length === 9) {
					uni.showToast({
						title:"最多选择9张图片"
					});
					return;
				}
				uni.chooseImage({
					sourceType: sourceType[this.sourceTypeIndex],
					sizeType: sizeType[this.sizeTypeIndex],
					count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList.length : this.count[this.countIndex],
					success: (res) => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
						//传递选择图片的事件
						this.$emit("upload-img",this.imageList);
					}
				});
			},
			previewImage: function(e) {
				var current = e.target.dataset.src
					uni.previewImage({
						current: current,
						urls: this.imageList
				});
			},
			deleteImage:function(index){	//删除选中的图片
				//提示确认
				uni.showModal({
					content: '确定删除这张图片?',
					success: (res) => {
						if (res.confirm) {
							//确定 删除这张图片
							this.imageList.splice(index,1);
							//传递选择图片的事件
							this.$emit("upload-img",this.imageList);
						} else if (res.cancel) {
							//取消  什么都不做
						}
					}
				});
			}
		}
	}
</script>

<style scoped>
	.cell-pd {
		padding: 22upx 30upx;
	}
	
	.list-pd {
		margin-top: 50upx;
	}
	/**
	 * 删除按钮的样式
	 */
	.uni-uploader__file{
		position: relative;
	}
	.img-delete{
		position: absolute;
		top: 0rpx;
		right: 0rpx;
		background-color: #6D6D72;
		opacity: 0.5;
		color: #FFFFFF;
		padding: 0rpx 10rpx;
		border-radius: 10rpx;
	}
</style>
