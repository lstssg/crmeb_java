<template>
	<scroll-view>
		<block v-for="(item,index) in goodsList" :key="index">
			<view class="goods" @tap="chooseGoods(item)">
				<image class="goodsPic" src="../../static/images/1-001.png" :src="item.goodsPic" mode="aspectFit"></image>
				<text>{{item.goodsName}}</text>
			</view>
		</block>
	</scroll-view>
</template>

<script>
	import {
		getProductslist,
		getProductHot
	} from '@/api/store.js';
	export default {
		data() {
			return {
				goodsList: [],
			}
		},
		onLoad() {
			var that = this;
			getProductslist().then(res => {
				let list = res.data.list;
				let _goodsList = [];
				
				// console.log('选择---' + list[0].image)
				list.forEach(function(item, index) {
					let goods = {
						goodsPic: '',
						goodsName: '',
						goodsId: ''
					}
					goods.goodsPic = list[index].image;
					goods.goodsName = list[index].storeName;
					goods.goodsId = list[index].id;
					_goodsList.push(goods);
				});
				that.goodsList = _goodsList;
				
			}).catch(err => {
				console.log("获取数据错误--->>>" + err)
			});
		},
		methods: {
			chooseGoods(e) {
				console.log("选择的商品是--->>>: ", e.goodsName);
				uni.navigateBack({
					
				})
				uni.$emit('choosenCommitGoods', {
					goodsId: e.goodsId,
					goodsName: e.goodsName,
					goodsPic: e.goodsPic
				});
			}
		}
	}
</script>

<style>
	.goods {
		width: 96%;
		height: 200rpx;
		margin-left: 2%;
		margin-right: 2%;
		margin-bottom: 30rpx;
		padding: 10rpx;
		border: 1rpx solid grey;
		border-radius: 10rpx;
		display: flex;
		align-items: center;
	}

	,

	.goodsPic {
		width: 180rpx;
		height: 180rpx;
		margin-right: 10rpx;
	}
</style>
