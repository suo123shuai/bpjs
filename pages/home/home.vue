<template>
	<view>
		<!-- <scroll-view scroll-x class="bg-white nav" scroll-with-animation :scroll-left="scrollLeft">
			<view class="cu-item" :class="index==TabCur?'text-green cur':''" v-for="(item,index) in title" :key="index" @tap="tabSelect" :data-id="index">
				{{item}}
			</view>
		</scroll-view> -->
		<view class="cu-bar bg-white solid-bottom" style="margin-top: 2px;z-index: 200;">
			<view class="action">
				<text class="cuIcon-title text-orange "></text> 快速通道
			</view>
		</view>
		<view class="cu-list grid col-4 no-border">
			<view class="cu-time"  v-for="(item,index) in iconList" :key="index" @tap="alt" :data-tabc="item">
				<image class="logo" :src="item.icon"></image>
			</view>
		</view> 
			
			
		<view ref="scroll1" class="flex solid-bottom padding justify-start" >
			<view class="bg-white">
				<view class="flex solid-bottom padding justify-around">
					<view class="uni-title uni-common-mt">
						<text>维修保养消息</text>
					</view>
					<view class="uni-title uni-common-mt">
						<text>提车消息</text>
					</view>
				</view>
				<view class="flex solid-bottom padding align-start ">
					<!-- <scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltolower="chudi"
							 style="height: 400rpx;background-color: #C8C7CC;" @scroll="scroll">
					</scroll-view>
					<scroll-view :scroll-top="scrollTop" scroll-y="true" class="scroll-Y" @scrolltolower="chudi"
						 style="height: 400rpx;margin-left: 5rpx;background-color: #C8C7CC;" @scroll="scroll">
						<div v-for='(item,index) in items' :key="index"  class="scroll-view-item zimo" >中奖人的名字是--{{item.name}}</div>
					</scroll-view> -->
					<view class="home" style="height: 400rpx;background-color: #C8C7CC;">
						<tony-scroll :list="items"></tony-scroll>
					</view>
					<view class="home" style="height: 400rpx;background-color: #C8C7CC;margin-left: 20rpx">
						<tony-scroll :list="items"></tony-scroll>
					</view>
				</view>
				
			</view>
		</view>
	</view>

</template>

<script>
import tonyScroll from '@/components/tony-scroll/tony-scroll.vue';
    var that;
	export default {
		data() {
			return {
				title: ['首页','用户维护','用户管理','角色维护','角色菜单维护','组织机构'],
				TabCur: 0,
				scrollTop: -1,
				top:0,
				old: {
					scrollTop: 0
				},
				scrollLeft: 0,
				Height: 200,
				items:[ //消息列表对应的数组
				{name:"您有一条来自于吴欣楠的待审批车辆申请您有一条来自于吴欣楠的待审批车辆申请"},
				{name:"雷军"},
				{name:"王勤1"},
				{name:"王勤2"},
				{name:"王勤3"},
				{name:"王勤4"},
				{name:"王勤5"},
				],
				gridCol:3,
				 iconList: [{
				      icon: require("../../static/home/qiangxiangongcheng.png"),
				      color: 'red',
				      name: '抢险工程',
					  url:'qianxian'
				    }, {
				      icon: require("../../static/home/wuliaoxinxi.png"),
				      color: 'orange',
				      badge: 1,
				      name: '物料信息'
				    }, {
				      icon: require("../../static/home/kufangweihu.png"),
				      color: 'yellow',
				      badge: 0,
				      name: '库房维护'
				    }, {
				      icon: require("../../static/home/cheliangdangan.png"),
				      color: 'olive',
				      badge: 22,
				      name: '车辆档案'
				    }, {
				      icon: require("../../static/home/cheliangweixiu.png"),
				      color: 'cyan',
				      badge: 0,
				      name: '车辆维修管理'
				    }, {
				      icon: require("../../static/home/cheliangzuling.png"),
				      color: 'blue',
				      badge: 0,
				      name: '车辆租赁'
				    }, {
				      icon: require("../../static/home/nianjianjilu.png"),
				      color: 'purple',
				      badge: 0,
				      name: '年检记录'
				    },
					{
					  icon: require("../../static/home/xitong.png"),
					  color: 'purple',
					  badge: 0,
					  name: '系统设置'
					}],
			}
		},
		onLoad() {
			that = this;
			// this.items = this.items.concat(this.items);
			// this.lower().then(() => {
				
			// });
			// setInterval(this.lower,100)
			// setInterval(() => {
			// 	this.$nextTick(function() {
			// 		this.lower();
			// 		console.log("wwwwwwwwwww")
			// 	})
			// },100)
		},
		mounted () {
		},
		components: {
			tonyScroll
		},
		methods: {
			tabSelect(e){
				this.TabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 100
			},
			alt(e){
				console.log(e)
				uni.navigateTo({
				    url: '/pages/'+e.currentTarget.dataset.tabc.url+'/home'
				});
			},
		},
		onShow:function(){
			that.items = that.items.concat(that.items);
		}
	}
</script>

<style>
	.logo{
		width: 110rpx;
		height: 160rpx;
	}
	.zimo{
		margin: 10rpx;
		padding: 10rpx;
		border: #FFFFFF solid 1rpx;
		border-radius: 10rpx;
		background-color: #FFFFFF;
	}
	.home{
		overflow:hidden;
	}
	
</style>
