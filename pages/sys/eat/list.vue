<template>
	<view class="wrap">
		<view class="search">
			<u-search v-model="keywords" @custom="search" @search="search"></u-search>
		</view>
		<scroll-view class="scroll-list" scroll-y="true">
			<view v-for="(item,index) in eatList" :key="index">
				<view class="uni-list">
					<uni-view class="uni-list-cell">
						<view class="uni-media-list" @click="navTo('/pages/sys/msg/list-item')">
							
							<image style="width: 80px; height: 80px; background-color: #eeeeee;" :mode="item.mode" :src="item.displayPicture"
							                        @error="imageError"></image>
							
							<!-- <view class="home-icon icon-color02">
								<i class="iconfont icon-tongzhi1">
									<u-badge type="error" count="3"></u-badge>
								</i>
							</view> -->
							<uni-view class="uni-media-list-body">
								<uni-view class="uni-media-list-text-top"><span>{{item.name}}</span><span
										style="font-size: 26rpx;color: #999999;">{{item.createTime}}</span></uni-view>
								<uni-view class="uni-media-list-text-bottom">
									<uni-text><span>{{item.description}}</span></uni-text>
								</uni-view>
							</uni-view>
						</view>
					</uni-view>
				</view>
				
				
			</view>
		</scroll-view>
	</view>
</template>
<script>
	import HeadNavBar from '@/components/headnavbar/index';
	/**
	 * Copyright (c) 2013-Now http://aidex.vip All rights reserved.
	 */
	export default {
		components: {
			HeadNavBar
		},
		data() {
			return {
				form: {

				},
				switchValue: false,
				sliderValue: 0,
				eatList: [],
			};
		},
		onLoad(option) {
			this.switchValue = option.switchValue;
			this.sliderValue = option.sliderValue;
			this.getRandomList()
		},
		methods: {
			getRandomList() {
				console.log("this.sliderValue", this.sliderValue);
				console.log("this.switchValue", this.switchValue);
				this.$u.api.eat.listEat({
						pageNum: 1,
						pageSize: 10
					})
					.then(res => {
						if (res.msg) {
							this.$u.toast(res.msg);
						}
						if (res.code == '200') {
							console.log('getRandomList： ', res)
							this.eatList = res.rows;
						}
					});
			},
			navTo(url) {
				uni.navigateTo({
					url: url
				});
			},
			search(value) {
				this.$u.toast('搜索内容为：' + value)
			}
		}
	};
</script>

<style lang="scss">
@import '../../../common/uni.css';
page {
	background-color: #f5f5f5;
}
.wrap .search{
	background: #ffffff;
}
.uni-title{
	font-size: 30rpx;
	color: #333333;
	padding: 10px;
	background: #fff;
	border-top:1px solid #ededed;
	margin-top: 20rpx;
}
.uni-media-list {
    padding: 15px 15px;

}
.uni-media-list-body {
    height: 42px;
	padding-left:20rpx;
}
.uni-media-list-text-top{
	height: 40rpx;
    overflow: hidden;
	width: 100%;
	line-height: 40rpx;
	font-size: 32rpx;
	display: flex;
	justify-content: space-between;
}

.uni-media-list-text-bottom {
    width: 100%;
    line-height: 24rpx;
    font-size: 26rpx;
	color: #666666;
	span{
		margin-right: 10rpx;
	}
}


</style>
