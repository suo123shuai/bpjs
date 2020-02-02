<template>
	<view>
		<map style="width:100%;height:85vh;" latitude="40.918973" longitude="118.398115"
		:markers="map.markers" @callouttap="qipao"></map>
	</view>
</template>

<script>
	
	export default {
		data() {
			return{
			　　// 经纪人id
			　　agentId:0,
			　　title: 'map',
			　　latitude: 40.013305,  //纬度
			　　longitude: 118.685713,  //经度
				map:{
					markers:[
						{
						id:0,
						latitude :"39.918973",
						longitude :"116.398115",
						iconPath:"/static/map/qx.png",
						width:40,
						height:40,
						callout:{
							content :"试试说",
							display :'BYCLICK',
							color:"#ffff"
						}
					},
					{
						id:1,
						latitude :"40.918983",
						longitude :"118.398125",
						iconPath:"/static/map/qx.png",
						width:40,
						height:40,
						callout:{
							content :"试试说",
							display :'BYCLICK',
							color:"#ffff"
						}
					}]
				}
			　}　　　　　　　　　　 
		},
		
		methods: {
			// biaoji(e){
			// 	// console.log(e.detail.markerId);
			// 	console.info(e)
			// },
			qipao(e){
				console.info(e)
			}
		}
	}
</script>

<style>

</style>
