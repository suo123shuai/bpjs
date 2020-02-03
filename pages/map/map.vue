<template>
	<view>
		<map style="width:100%;height:100vh;" latitude="39.918973" longitude="116.398115"
		:markers="map.markers" @callouttap="qipao"></map>
	</view>
</template>

<script>
	
	export default {
		data() {
			return{
			　　	map:{
					markers:[
						{
						id:0,
						latitude :39.918973,
						longitude :116.398115,
						iconPath:"/static/map/xqx.png",
						
						callout:{
							content :"试试说",
							display :'BYCLICK',
							color:"#ffff"
						}
					},
					{
						id:1,
						latitude :"39.918984",
						longitude :"116.398216",
						iconPath:"/static/map/xqx.png",
						callout:{
							content :"试试说",
							display :'BYCLICK',
							color:"#ffff"
						}
					}
					]
				}
			　}　　　　　　　　　　 
		},
		
		methods: {
			// biaoji(e){
			// 	// console.log(e.detail.markerId);
			// 	console.info(e)
			// },
			qipao(e){
				// console.info(e)
				let s = e.detail.markerId;
				console.log(e)
				// uni.navigateTo({
				//     url: '../xianxi/xianxi'
				// });
			}
		}
	}
</script>

<style>

</style>
