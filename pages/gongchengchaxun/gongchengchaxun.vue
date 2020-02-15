<template>
	<view>
		<!-- <view class="example-body"> -->
			<!-- <uni-nav-bar left-icon="arrowleft" right-text="菜单" left-text="返回" title="标题" @clickLeft="back" :fixed="true" :status-bar="true"/> -->
		<!-- </view> -->
		<view class="example-body">
			<uni-nav-bar background-color="#F8F8F8" :status-bar="true" right-text="搜索" left-icon="arrowleft"  title="工程查询" @clickLeft="back" style="font-size:10rpx" @clickRight="open"/>
		</view>
		<!-- <scroll-view scroll-x class="bg-white nav text-center">
		  <view class="cu-item text-blue cur" v-for="(item, index) in 3" :key="index" @tap="tabSelect">
		    Tab{{index}}
		  </view>
		</scroll-view> -->
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
		
		<view class="cehua">
			<hj-dragabledrawer :options="options" ref="dragBox" @open="afterOpen" @close="afterClose">
				<!-- <button @tap="hello">hi</button> -->
				<view @tap="close" style="white:10rpx;height:50rpx;margin-top: 50rpx;margin-left: 50rpx;">
					x
				</view>
				<view style="margin-top: 50rpx;"> 
					<form @submit="formsu" @reset="re">
						<view class="input-view">
							<label class="la">管网分公司:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">工程名称:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">项目部:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">工程状态:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">性质:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">管径(mm):</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">事故原因:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
						<view class="input-view">
							<label class="la">施工方案:</label>
							<view class="input">
								<input name="guanwan"  />
							</view>
						</view>
					</form>
				</view>
				
				<button @tap="close">关闭</button>
			</hj-dragabledrawer>
			<!-- <button @tap="open">打开</button> -->
		</view>
	</view>
</template>
<script>
	import uniDrawer from '@/components/uni-drawer/uni-drawer.vue'
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	import hjDragabledrawer from '@/components/hj-dragabledrawer/hj-dragabledrawer.vue' //这里修改下插件的相对路径
	let dragBox;
	export default {
		components: {
			uniDrawer,
			hjDragabledrawer,
			uniNavBar,
		},
		data() {
			return {
				showRight: false,
				options: {
					visible: false,
					rightMode: true,
					autoClose: false
				}
			}
		},
		onReady() {
			dragBox = this.$refs.dragBox;
		},
		methods: {
			// show() {
			// 	this.showRight = true;
			// },
			// closeDrawer(){
			// 	this.showRight = false;
			// },
			open() {
				dragBox.open()
			},
			// hello() {
			// 	uni.showToast({
			// 		title: 'hello',
			// 		icon: 'none',
			// 	});
			// },
			close(){
				dragBox.close()
			},
			toggle() {
				this.options.rightMode = !this.options.rightMode
			},
			toggle1() {
				this.options.autoClose = !this.options.autoClose
			},
			// afterOpen() {
			// 	uni.showToast({
			// 		title: 'open',
			// 		icon: 'none',
			// 	});
			// },
			// afterClose() {
			// 	uni.showToast({
			// 		title: 'close',
			// 		icon: 'none',
			// 	});
			// },
			back(){
				uni.navigateBack({
				    delta: 1
				});
			}
		},
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
	.la{
		width: 40%;text-align:right;line-height: 50rpx;
	}
	.cehua{
		height: 80%;
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
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		padding: 0;
		font-size: 4rpx;
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
		
		flex-direction: row;
		height: 100rpx;
		
		/* background-color: #e7e7e7;
		height: 30px;
		border-radius: 15px;
		padding: 0 10px;
		flex: 1;
		background-color: #f5f5f5; */
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
		/* flex: 1;
		padding: 0 5px;
		height: 24px;
		line-height: 24px;
		font-size: 28rpx;
		background-color: transparent; */
		width: 50%;
		height: 50rpx;
		border: #EBEEF5 solid 2rpx;
		margin-left: 20rpx;
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