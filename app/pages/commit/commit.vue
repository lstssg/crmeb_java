<template>
	<form @submit="formSubmit">
		<view>
			<view class="content">
				<textarea class="ta" maxlength="1000" placeholder="请输入想说的话..." @blur="bindTextAreaBlur" />
				</view>
		<view class="preViewAll">
		<!--图片-->
		<view v-for="(item,index) in imageList" :key="index">
			<view class="imagePreview">
				<image style="width:165rpx;height:165rpx;border-radius: 15rpx;" :src="item" @tap="previewImage"></image>
				<view style="position:absolute; right: -10rpx; top: -10rpx; z-index:1000;" @tap="delect(index)">
					<image src="../../static/images/del.png" style="width:50rpx;height:50rpx;" mode=""></image>
					<!--这个图标是指，图片或者视频上传成功了，点击右上角叉号（也就是这个图标）可以删除 这里自己找一个合适的替换掉就好-->
				</view>
			</view>
		</view>
		<!--视频-->
		<view v-for="(item1, index1) in srcVideo" :key="index1">
			<view class="videoPreview">
				<video style="width:165rpx;height:165rpx;border-radius: 15rpx;" :src="item1"></video>
				<view style="position:absolute; right: -10rpx; top: -10rpx; z-index:1000;" @tap="delectVideo(index1)">
					<image style="width:50rpx;height:50rpx;" src="../../static/images/del.png" mode=""></image>
				</view>
			</view>
		</view>
		<view class="uploadButton" v-if="VideoOfImagesShow" @tap="chooseVideoImage">
			<image src="../../static/images/paizhao.png" style="width:100rpx;height:100rpx;border-radius: 15rpx;" mode=""></image>
			<view style="font-size:30rpx;">拍照/视频</view>
		</view>
	</view>
	<view class="sendView">
			<button class="send" formType="submit">
				<text class="sendText">发送</text>
			</button>
	
	</view>
	</view>
</form>
</template>

<script>
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	];
	export default {
		data() {
			return {
				VideoOfImagesShow: true, // 页面图片或视频数量超出后，拍照按钮隐藏
				imageList: [], //存放图片的地址
				srcVideo: [], //视频存放的地址
				sourceType: ['拍摄', '相册', '拍摄或相册'],
				sourceTypeIndex: 2,
				cameraList: [{
					value: 'back',
					name: '后置摄像头',
					checked: 'true'
				}, {
					value: 'front',
					name: '前置摄像头'
				}],
				cameraIndex: 0, //
				
				inputVal:""
			}
		},
		onUnload() {
			(this.imageList = []), (this.sourceTypeIndex = 2), (this.sourceType = ['拍摄', '相册', '拍摄或相册']);
		},
		methods: {
			//点击上传图片或视频
			chooseVideoImage() {
				uni.showActionSheet({
					title: '选择上传类型',
					itemList: ['图片', '视频'],
					success: res => {
						console.log(res);
						if (res.tapIndex == 0) {
							this.chooseImages();
						} else {
							this.chooseVideo();
						}
					}
				});
			},
			//上传图片
			chooseImages() {
				uni.chooseImage({
					count: 4, //默认是9张
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album', 'camera'], //从相册选择
					success: res => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
						console.log(this.imageList)
						if (this.imageList.length == 4) {
							this.VideoOfImagesShow = false; //图片上传数量和count一样时，让点击拍照按钮消失
						}
					}
				})
			},
			//上传视频
			chooseVideo() {
				uni.chooseVideo({
					maxDuration: 60, //拍摄视频最长拍摄时间，单位秒。最长支持 60 秒
					count: 4,
					camera: this.cameraList[this.cameraIndex].value, //'front'、'back'，默认'back'
					sourceType: sourceType[this.sourceTypeIndex],
					success: res => {
						this.srcVideo = this.srcVideo.concat(res.tempFilePath);
						if (this.srcVideo.length == 4) {
							this.VideoOfImagesShow = false;
						}
						console.log(this.srcVideo);
					}
				})
			},
			//预览图片
			previewImage: function(e) {
				var current = e.target.dataset.src;
				uni.previewImage({
					current: current,
					urls: this.imageList
				});
			},
			// 删除图片
			delect(index) {
				uni.showModal({
					title: '提示',
					content: '是否要删除该图片',
					success: res => {
						if (res.confirm) {
							this.imageList.splice(index, 1);
						}
						if (this.imageList.length == 4) {
							this.VideoOfImagesShow = false;
						} else {
							this.VideoOfImagesShow = true;
						}
					}
				});
			},
			// 删除视频
			delectVideo(index) {
				uni.showModal({
					title: '提示',
					content: '是否要删除此视频',
					success: res => {
						if (res.confirm) {
							this.srcVideo.splice(index, 1);
						}
						if (this.srcVideo.length == 4) {
							this.VideoOfImagesShow = false;
						} else {
							this.VideoOfImagesShow = true;
						}
					}
				});
			},
			
			bindTextAreaBlur: function (e) {
			    
			    this.inputVal = e.detail.value;
			  },
			  //内容由于只能通过表单获取在这里发送
			  formSubmit: function (e) {
				  console.log(this.inputVal);
			    // this.sendContent(this.data.inputVal);
			  },
		}
	}
</script>

<style>
	.preViewAll {
		width: 740rpx;
		height: auto;
		margin-top: auto;
		display: flex;
		justify-content: flex-start;
		flex-wrap: wrap;
	}

	,
	.uploadButton {
		width: 165rpx;
		height: 165rpx;
		margin-left: 15rpx;
		margin-top: 15rpx;
		border-radius: 15rpx;
		background-color: #F1F1F1;
		/* margin: 20rpx auto 0; */
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
	}

	,
	.imagePreview {
		position: relative;
		width: 165rpx;
		height: 165rpx;
		margin-left: 15rpx;
		margin-top: 15rpx;
		border-radius: 15rpx;
		/* margin: 20upx 0 20upx 0; */
	}

	,
	.videoPreview {
		position: relative;
		width: 165rpx;
		height: 165rpx;
		margin-left: 15rpx;
		margin-top: 15rpx;
		border-radius: 15rpx;
	},
	.content{
		background-color: white;
		 width: 98%;
		 margin-left: 1%;
		 margin-right: 1%;
		 margin-top: 15rpx;
		
	},
	.ta{
		width: 98%;
		margin-left: 1%;
		margin-right: 1%;
		font: 'Courier New', Courier, monospace;
		font-size: medium;
	},
	.send {
	  background-color: #F76968;
	  width: 80%;
	  height: 100rpx;
	  margin-top: 80rpx;
	  margin-right: 10%;
	  margin-left: 10%;
	  border-radius: 10rpx;
	  display: flex;
	  align-items: center;
	  justify-content: center;
	}
	
	.sendText {
	  font-size: 30rpx;
	  color: white;
	}
</style>
