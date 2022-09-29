<template>
	<view class="wrap">
		<form @submit="onSubmit">
			<view class="title">这顿吃什么</view>
			<view class="content">点一下解决你的吃饭难题，吃什么不用愁！</view>
			<view class="several_dishes">是否有汤</view>
			<switch class="switch" checked v-model="switchValue" @change="switchChange" active-color="#13ce66" inactive-color="#ff4949">
			</switch>
			<view class="several_dishes">几个菜</view>
			<view>
				<slider value="2" @change="sliderChange" min="1" max="6" show-value />
			</view>
			
			<u-button form-type="primary" class="c_button"  @click="onSubmit" :hair-line="false">开始</u-button>
		</form>

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
			};
		},
		onLoad() {

		},
		methods: {
			navTo(url) {
				uni.navigateTo({
					url: url + '?sliderValue=' + this.sliderValue + '&switchValue=' + this.switchValue
				});
			},
			switchChange(e) {
				this.switchValue = e.detail.value;
				console.log('switchValue： ' + this.switchValue)
				
			},
			sliderChange(e) {
				console.log('sliderChange 发生变化：' + e.detail.value)
				this.sliderValue = e.detail.value;
			},
			onSubmit(e) {
				console.log("this.sliderValue", this.sliderValue)
				console.log("this.switchValue", this.switchValue)
				// "navTo('/pages/sys/eat/list')"
				this.navTo('/pages/sys/eat/list');
			}

		}
	};
</script>
<style lang="scss">
	@import 'index.scss';

	.wrap {
		width: 100%;
		height: 100%;
		background: yellow;
		position: absolute;
		background: url('/static/aidex/images/eat_background.jpg') no-repeat;
		background-size: 100% 100%;
	}

	.title {
		font-size: 50rpx;
		font-weight: bold;
		color: #333333;
		padding: 15px 30rpx;
		text-align: center;
		margin-top: 60rpx;
	}

	.content {
		font-size: 35rpx;
		font-weight: bold;
		color: #333333;
		padding: 15px 30rpx;
		text-align: center;
		margin-top: 100rpx;
	}

	.switch {
		display: block;
		padding: 15px 30rpx;
		text-align: center;
	}

	.several_dishes {
		font-size: 40rpx;
		font-weight: bold;
		color: #333333;
		padding: 15px 30rpx;
		text-align: center;
		margin-top: 30rpx;
	}

	.c_button {
		margin-top: 50rpx;
	}
</style>
