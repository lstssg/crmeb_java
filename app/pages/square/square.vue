<template>
	<view class="content">
		<waterfallsFlow :list="list" ref="waterfallsFlow" @wapper-lick="wapperClick" @image-load="imgLoad">
			<!--  #ifdef  MP-WEIXIN -->
			<view v-for="(item,index) of list" :key="index" slot="slot{{index}}">
				<view class="cnt">
					<view class="title">{{item.title}}</view>
					<view class="text">{{item.text}}</view>
					<view class="bottomInfo">
						<view class="user">
							<image class="picHead" src="../../static/images/member.png"></image>
							<text class="goodNum">{{item.id}}</text>
						</view>

						<view class="good">
							<image class="picHead" src="../../static/images/member.png"></image>
							<text class="goodNum">0</text>
						</view>
					</view>
				</view>
			</view>
			<!--  #endif -->

			<!-- #ifndef  MP-WEIXIN -->
			<template v-slot:default="item">
				<view class="cnt">
					<view class="title">{{item.title}}</view>
					<view class="text">{{item.text}}</view>
					<view class="bottomInfo">
						<view class="user">
							<image class="picHead" src="../../static/images/member.png"></image>
							<text class="goodNum">{{item.id}}</text>
						</view>
					
						<view class="good">
							<image class="picHead" src="../../static/images/member.png"></image>
							<text class="goodNum">0</text>
						</view>
					</view>
				</view>
			</template>
			<!-- #endif -->
		</waterfallsFlow>
		<view class="no-more" v-if="isEnd">没有更多了</view>
	</view>
</template>

<script>
	import waterfallsFlow from "@/components/maramlee-waterfalls-flow/maramlee-waterfalls-flow.vue";
	export default {
		components: {
			waterfallsFlow
		},
		onPullDownRefresh() {
			console.log("触发下拉刷新: ");
			this.$refs.waterfallsFlow.refresh();
			// 重新获取渲染列表
			uni.startPullDownRefresh({
				complete() {
					console.log("刷新完成---: ");
				}
			})
		},
		onReachBottom() {
			setTimeout(() => {
				this.list = this.list.concat(this.$data.list2);
				
			},500)
		},
		data() {
			return {
				list: [{
						id: 1,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599475741266&di=e36d6c01c93320e2ba1504d8357248f4&imgtype=0&src=http%3A%2F%2Fa0.att.hudong.com%2F30%2F29%2F01300000201438121627296084016.jpg",
						title: "可爱的小猫咪呀",
						text: "小小的猫咪，甚是呆萌，呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌",
					},
					{
						id: 2,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599475934834&di=7a37b8d628252c4aced6ed0decba9442&imgtype=0&src=http%3A%2F%2Fa3.att.hudong.com%2F43%2F74%2F01300000164151121808741085971.jpg",
						title: "迪士尼动画",
						text: "迪士尼动画之……",
					},
					{
						id: 3,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476083909&di=a5debff35edec5de105bc105d6fdbce3&imgtype=0&src=http%3A%2F%2Fa2.att.hudong.com%2F77%2F77%2F01300000336597125202779973172.jpg",
						title: "火箭",
						text: "火箭升空瞬间，宏伟壮观啊",
					},
					{
						id: 5,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476129760&di=7a3db0b14f6a74240bbfa7922ba22f45&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F82%2F55%2F01300000349330124003555691086.jpg",
						title: "华佗",
						text: "华佗人物画像 中国画 线条画 毛笔画 彩色画",
					},
					{
						id: 6,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476215687&di=97c2bbf6f3a1a3e2a6a2dc77dfe4bea7&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F72%2F82%2F19300000009075130804824786610.jpg",
						title: "恐龙",
						text: "恐龙来啦",
					},
					{
						id: 7,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605171733299&di=026dd8bc87bea2dea438d574aac11975&imgtype=0&src=http%3A%2F%2Ffile.elecfans.com%2Fweb1%2FM00%2F7D%2F39%2Fo4YBAFwJ4Y2AJ5SmAAdIU_6oLS8339.png",
						title: "网络",
						text: "网络发散？",
					},
					{
						id: 8,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476300222&di=49712f992d8f7bbb1a5851eced71cbe2&imgtype=0&src=http%3A%2F%2Fa2.att.hudong.com%2F71%2F56%2F16300000988660128426569668958.jpg",
						title: "百年好合",
						text: "百年好合 结婚 庚帖 二次元",
					},
					{
						id: 9,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476416001&di=ea1a1f8f9b1274d39c05af3e48041e6a&imgtype=0&src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F12420002963%2F641",
						title: "5G",
						text: "5G 来啦",
					},
					{
						id: 10,
						image_url: "https://www.404.com/404.png",
						title: "404",
						text: "404",
					},
					{
						id: 12,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476567983&di=040976a1cd1a6e5510a237c57bdcff06&imgtype=0&src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F12421051168%2F641",
						title: "王者荣耀",
						text: "王者荣耀 龙 快来打龙 请求集合",
					},
				],
				list2: [{
						id: 13,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599475741266&di=e36d6c01c93320e2ba1504d8357248f4&imgtype=0&src=http%3A%2F%2Fa0.att.hudong.com%2F30%2F29%2F01300000201438121627296084016.jpg",
						title: "可爱的小猫咪呀",
						text: "小小的猫咪，甚是呆萌，呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌呆萌",
					},
					{
						id: 14,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599475934834&di=7a37b8d628252c4aced6ed0decba9442&imgtype=0&src=http%3A%2F%2Fa3.att.hudong.com%2F43%2F74%2F01300000164151121808741085971.jpg",
						title: "迪士尼动画",
						text: "迪士尼动画之……",
					},
					{
						id: 15,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476083909&di=a5debff35edec5de105bc105d6fdbce3&imgtype=0&src=http%3A%2F%2Fa2.att.hudong.com%2F77%2F77%2F01300000336597125202779973172.jpg",
						title: "火箭",
						text: "火箭升空瞬间，宏伟壮观啊",
					},
					{
						id: 16,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476129760&di=7a3db0b14f6a74240bbfa7922ba22f45&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F82%2F55%2F01300000349330124003555691086.jpg",
						title: "华佗",
						text: "华佗人物画像 中国画 线条画 毛笔画 彩色画",
					},
					{
						id: 17,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476215687&di=97c2bbf6f3a1a3e2a6a2dc77dfe4bea7&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F72%2F82%2F19300000009075130804824786610.jpg",
						title: "恐龙",
						text: "恐龙来啦",
					},
					{
						id: 18,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605171733299&di=026dd8bc87bea2dea438d574aac11975&imgtype=0&src=http%3A%2F%2Ffile.elecfans.com%2Fweb1%2FM00%2F7D%2F39%2Fo4YBAFwJ4Y2AJ5SmAAdIU_6oLS8339.png",
						title: "网络",
						text: "网络发散？",
					},
					{
						id: 19,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476300222&di=49712f992d8f7bbb1a5851eced71cbe2&imgtype=0&src=http%3A%2F%2Fa2.att.hudong.com%2F71%2F56%2F16300000988660128426569668958.jpg",
						title: "百年好合",
						text: "百年好合 结婚 庚帖 二次元",
					},
					{
						id: 20,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476416001&di=ea1a1f8f9b1274d39c05af3e48041e6a&imgtype=0&src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F12420002963%2F641",
						title: "5G",
						text: "5G 来啦",
					},
					{
						id: 21,
						image_url: "https://www.404.com/404.png",
						title: "404",
						text: "404",
					},
					{
						id: 22,
						image_url: "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1599476567983&di=040976a1cd1a6e5510a237c57bdcff06&imgtype=0&src=http%3A%2F%2Finews.gtimg.com%2Fnewsapp_bt%2F0%2F12421051168%2F641",
						title: "王者荣耀",
						text: "王者荣耀 龙 快来打龙 请求集合",
					},
				],
				isEnd : true,
			};
			
		},
		methods: {
			wapperClick(e) {
				console.log("点击了wapper---" + e.id);
			},
			imgLoad(){
				console.log("图片加载完毕---: ");
				uni.hideLoading();
			}
		}
	};
</script>
<style>
	page {
		background-color: #eee;
	}
</style>
<style lang="scss" scoped>
	.content {
		padding: 10rpx;

		.cnt {
			// padding: 10px;
			padding-left: 10rpx;
			padding-right: 10rpx;

			.title {
				font-size: 16px;
			}

			.text {
				font-size: 14px;
				margin-top: 5px;
			}
		}
	}

	,
	.bottomInfo {
		margin-top: 20rpx;
		display: flex;
		align-items: flex-start;
		justify-content: flex-start;
	}

	,
	.user{
		display: flex;
	}
	.good {
		display: flex;
		margin-left: auto;
		margin-right: 20rpx;
	}

	,
	.goodNum {
		font-size: 40rpx;
		margin-left: 15rpx;
	}

	,
	.picHead {
		width: 50rpx;
		height: 50rpx;
	},
	.no-more {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	  font-size: 24rpx;
	  color: #8799a3;
	  margin-top: 20rpx;
	  margin-bottom: 50rpx;
	}
</style>
