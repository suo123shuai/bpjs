<template>
	<view>
		<scroll-view scroll-x class="bg-white nav text-center">
		  <view class="cu-item text-blue cur" v-for="(item, index) in 3" :key="index" @tap="tabSelect">
		    Tab{{index}}
		  </view>
		</scroll-view>
		<view class="fenkuai" @tap="tiao" >
			<view>
				管网分公司:管网一分
			</view>
			<view>
				拟定工程名称:景泰路污水抢险工程
			</view>
			<view>
				事件发生地点:北京市东城区永定门外街道景泰路李村
			</view>
			<view>
				处置开始时间:2020-01-06 22:57:00
			</view>
			<view>
				处置完成时间:2020-01-06 22:57:00
			</view>
			<!-- <view>
				抢险负责人:王宝通
			</view>
			<view>
				工程状态:已完成
			</view> -->
		</view>
		
		<view class="example-body">
			<view class="word-btn draw-cotrol-btn" hover-class="word-btn--hover" :hover-start-time="20" :hover-stay-time="70" @click="show('right')"><text class="word-btn-white">显示Drawer</text></view>
			<uni-drawer :visible="showRight" mode="right" @close="closeDrawer('right')">
				
				
			</uni-drawer>
		</view>
	</view>
</template>
<script>
	import uniDrawer from '@/components/uni-drawer/uni-drawer.vue'
	import uniList from '@/components/uni-list/uni-list.vue'
	import uniListItem from '@/components/uni-list-item/uni-list-item.vue'
	import uniSection from '@/components/uni-section/uni-section.vue'
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	export default {
		components: {
			uniIcons,
			uniDrawer,
			uniList,
			uniListItem,
			uniSection
		},
		data() {
			return {
				showRight: false,
				showLeft: false
			}
		},
		methods: {
			show(e) {
				console.log("show", e);
				if (e === 'left') {
					this.showLeft = true
				} else {
					this.showRight = true
				}
			},
			hide() {
				console.log("hide");
				this.showLeft = false
				this.showRight = false
			},
			closeDrawer(e) {
				if (e === 'left') {
					this.showLeft = false
				} else {
					this.showRight = false
				}
			},
			confirm() {
				
			},
			tiao(){
				
			}
		},
		onNavigationBarButtonTap(e) {
			this.showRight = !this.showRight
		},
		onBackPress() {
			if (this.showRight || this.showLeft) {
				this.hide()
				return true
			}
		}
		
	}
</script>

<style>
	/* 头条小程序组件内不能引入字体 */
	/* #ifdef MP-TOUTIAO */
	@font-face {
		font-family: uniicons;
		font-weight: normal;
		font-style: normal;
		src: url('~@/static/uni.ttf') format('truetype');
	}

	/* #endif */

	/* #ifndef APP-NVUE */
	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #efeff4;
		min-height: 100%;
		height: auto;
	}

	view {
		font-size: 28rpx;
		line-height: inherit;
	}
	.fenkuai{
		width: 98%;
		margin-left: 1%;
		margin-top: 2%;
		padding: 20rpx 20rpx;
		border-radius: 20rpx;
		background-color: #FFFFFF;
	}
	.fenkuai view{
		margin-top: 2%;
	}

	.example {
		padding: 0 30rpx 30rpx;
	}

	.example-info {
		padding: 30rpx;
		color: #3b4144;
		background: #ffffff;
	}

	.example-body {
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		padding: 0;
		font-size: 14rpx;
		background-color: #ffffff;
	}

	/* #endif */
	.example {
		padding: 0 30rpx;
	}

	.example-info {
		/* #ifndef APP-NVUE */
		display: block;
		/* #endif */
		padding: 30rpx;
		color: #3b4144;
		background-color: #ffffff;
		font-size: 30rpx;
	}

	.example-info-text {
		font-size: 28rpx;
		line-height: 36rpx;
	}


	.example-body {
		flex-direction: column;
		padding: 30rpx;
		background-color: #ffffff;
	}

	.word-btn-white {
		font-size: 18px;
		color: #FFFFFF;
	}

	.word-btn {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		align-items: center;
		justify-content: center;
		border-radius: 6px;
		height: 48px;
		margin: 15px;
		background-color: #007AFF;
	}

	.word-btn--hover {
		background-color: #4ca2ff;
	}


	.header {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		padding: 10px 15px;
		align-items: center;
		border-top-width: 1px;
		border-top-color: #f5f5f5;
		border-top-style: solid;
		background-color: #ffffff;
	}

	.input-view {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		align-items: center;
		flex-direction: row;
		background-color: #e7e7e7;
		height: 30px;
		border-radius: 15px;
		padding: 0 10px;
		flex: 1;
		background-color: #f5f5f5;
	}

	.uni-drawer-info {
		background-color: #ffffff;
		padding: 30rpx;
		padding-top: 10rpx;
		color: #3b4144;
	}

	.uni-padding-wrap {
		padding: 0 15px;
		line-height: 1.8;
	}

	.input {
		flex: 1;
		padding: 0 5px;
		height: 24px;
		line-height: 24px;
		font-size: 28rpx;
		background-color: transparent;
	}

	.close {
		padding: 30rpx;
	}

	.example-body {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		padding: 0;
	}

	.draw-cotrol-btn {
		flex: 1;
	}
	
	.status_bar {
	      height: var(--status-bar-height);
	      width: 100%;
	  }
</style>