<template>
	<view>
		<!-- 饼状图-->
		<view class="qiun-columns">
			<view class="qiun-bg-white qiun-title-bar qiun-common-mt display-between" >
				<view class="qiun-title-dot-light">工程分析</view>
				<navigator url="../gongchengchaxun/gongchengchaxun">
					详细内容>>
				</navigator>
			</view>
			<view class="qiun-charts qiun-rows" >
				<canvas canvas-id="canvasPie" id="canvasPie" class="charts-pie" @touchstart="touchPie"></canvas>
			</view>
		</view>
		<!-- 柱状图-->
		<view class="qiun-columns" style="margin-top: 80rpx;">
			<view class="qiun-bg-white qiun-title-bar qiun-common-mt display-between" >
				<view class="qiun-title-dot-light">抢险工程</view>
				<navigator url="../gongchengchaxun/gongchengchaxun">
					详细内容>>
				</navigator>
			</view>
			<view class="qiun-charts" >
				<canvas canvas-id="canvasColumn" id="canvasColumn" class="charts" @touchstart="touchColumn"></canvas>
			</view>
		</view>
	</view>
</template>

<script>
	import uCharts from '@/components/u-charts/u-charts.js';
	var _self;
	var canvaPie=null;
	var canvaColumn=null;
   
	export default {
		data() {
			return {
				cWidth:'',
				cHeight:'',
				pixelRatio:1,
				serverData:'',
				piearr:[],
				series: [{
					"name": "管线老化,造成路面或步道塌陷",
					"data": 50,
					"legendShape":"rect"
				 }, {
					"name": "管线老化,造成路面或步道未塌陷",
					"data": 30,
					"legendShape":"rect"
				  }, {
					"name": "检查井井墙倒塌",
					"data": 20,
					"legendShape":"rect"
				  }, {
					"name": "盖板老化,造成路面或步道塌陷",
					"data": 18,
					"legendShape":"rect"
				  }, {
					"name": "盖板老化,造成路面或步道未塌陷",
					"data": 8
				  }, {
					"name": "外单位施工破坏",
					"data": 8
				  }, {
					"name": "雨水篦子倒塌",
					"data": 8,
					
				  }],
				chartData: {
				  "categories": ["东西城", "朝阳", "海淀", "丰台、石景山"],
				  "series": [{
					"name": "成交量1",
					"data": [92, 55, 73, 60]
				  }]
				}
			}
		},
		onLoad() {
			_self = this;
			this.cWidth=uni.upx2px(750);
			this.cHeight=uni.upx2px(550);
			this.getServerData();
			_self.showPie("canvasPie",_self.series);
			_self.showColumn("canvasColumn",_self.chartData);
		},
		methods: {
			getServerData(){

				// _self.showPie("canvasPie",_self.series);
			},
			showPie(canvasId,data){
				canvaPie=new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'pie',
					colors: ['#1890ff', '#2fc25b', '#facc14', '#f04864', '#90ed7d', '#8543e0', '#00ff00'],
					fontSize:11,
					legend:{
					  show:true,
					  // position:'right',
					  float:'center',
					  itemGap:10,
					  padding:5,
					  lineHeight:16,
					  margin:10,
					  borderWidth :1
					},
					background:'#FFFFFF',
					pixelRatio:_self.pixelRatio,
					series: data,
					animation: true,
					width: _self.cWidth*_self.pixelRatio + 20,
					height: _self.cHeight*_self.pixelRatio +20,
					dataLabel: true,
					extra: {
						pie: {
						  labelWidth:15
						}
					},
				});
				this.piearr=canvaPie.opts.series;
			},
			touchPie(e){
				canvaPie.showToolTip(e, {
					format: function (item) {
						
						return item.name + ':' + item.data 
					}
				});
				canvaPie.touchLegend(e, {
					format: function (item) {
						console.info(item)
					}
				});
				
			},
			showColumn(canvasId,chartData){
				canvaColumn=new uCharts({
					$this:_self,
					canvasId: canvasId,
					type: 'column',
					legend:{
						show:false,
						itemGap:1,
						lineHeight:5
					},
					fontSize:11,
					background:'#FFFFFF',
					pixelRatio:_self.pixelRatio,
					animation: true,
					categories: chartData.categories,
					series: chartData.series,
					xAxis: {
						disableGrid:true,
						fontSize:10,
						
					},
					yAxis: {
						//disabled:true
						min:0,
						max:100,
						splitNumber:5,
						padding:5
					},
					dataLabel: true,
					width: _self.cWidth*_self.pixelRatio-20,
					height: _self.cHeight*_self.pixelRatio-20,
					extra: {
						column: {
							type:'group',
							width: _self.cWidth*_self.pixelRatio*0.45/chartData.categories.length -10
						}
					  }
				});
				
			},
			touchColumn(e){
				canvaColumn.showToolTip(e, {
					format: function (item, category) {
						if(typeof item.data === 'object'){
							return category + ' ' + item.name + ':' + item.data.value 
						}else{
							return category + ' ' + item.name + ':' + item.data 
						}
					}
				});
			},
			
		}
	}
</script>

<style>
page{background:#FFFFFF;width: 100vw;overflow-x: hidden;}
.qiun-rows{display:flex; flex-direction:row !important;}
.qiun-columns{display:flex; flex-direction:column !important;}
.qiun-bg-white{background:#FFFFFF;}
.charts-pie{width: 98vw; height:40vh;background-color: #FFFFFF;}
.charts{width: 98vw; height:40vh;background-color: #FFFFFF;margin: 0upx 10upx;}
.qiun-common-mt{padding:20upx 20upx;}
.qiun-bg-white{background:#FFFFFF;}
.qiun-title-bar{width:100vw; flex-wrap:nowrap;}
.qiun-title-dot-light{border-left: 10upx solid #0ea391; padding-left: 10upx; font-size: 32upx;color: #000000}
.qiun-charts{width: 100vw; height:40vh;background-color: #FFFFFF;}
.display-between{display: flex; justify-content: space-between;}
</style>