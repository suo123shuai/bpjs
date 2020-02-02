<template>
	<view class="container">
		<view class="canvasView">
			<view canvasId="pie" ref="pieChart" id="main"></view>
		</view>
	</view>
</template>

<script>
	import * as echarts from '@/components/echarts/echarts.simple.min.js';
	import mpvueEcharts from '@/components/mpvue-echarts/src/echarts.vue';
	
	// 指定图表的配置项和数据
	        var option = {
	            title: {
	                text: 'ECharts 入门示例'
	            },
	            tooltip: {},
	            legend: {
	                data:['销量']
	            },
	            xAxis: {
	                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
	            },
	            yAxis: {},
	            series: [{
	                name: '销量',
	                type: 'bar',
	                data: [5, 20, 36, 10, 10, 20]
	            }]
	        };

	
	export default {
		data() {
			return {
				echarts: echarts,
				updateStatus: false
			}
		},
		onLoad() {

		},
		mounted() {
			echarts.init(document.getElementById('main')).setOption({
				series: {
					type: 'pie',
					data: [
						{name: 'A', value: 1212},
						{name: 'B', value: 2323},
						{name: 'C', value: 1919}
					]
				}
			});
		},
		methods: {
			
			
		},
		components: {
			
		}
	}
</script>

<style>
	page,
	view {
		display: flex;
        font-size: 28upx;
	}

	page {
		min-height: 100%;
	}

	.page-section-title {
		padding: 0 30upx;
	}

	.title {
		margin-left: 30upx;
        line-height: 1.5;
		color: #8f8f94;
	}

	.container {
		padding-bottom: 30upx;
		box-sizing: border-box;
	}

	.container,
	.canvasView {
		flex: 1;
		flex-direction: column;
	}

	.navigate {
		color: #007AFF;
	}

	.canvas-bar {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	.update-btn {
		margin-right: 30upx;
	}
</style>
