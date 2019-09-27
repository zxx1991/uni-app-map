<template>
	<view class="content">
		<map class="map_style" :latitude="latitude" :longitude="longitude" :markers="covers" v-if="map"></map>
		<div class="foot">
		    <!-- <label id="label">正在获取您的位置</label> -->
			<!-- <label id="label">经度：{{latitude}} 纬度：{{longitude}}</label> -->
			<label id="label">距离目的地: {{distence}} 米</label>
		    <button id="button" style="color: white;" v-if="!isTrue">签到</button>
			<button id="button" style="color: white;background: #515151;" v-if="isTrue">签到</button>
		</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			  isTrue:false,//是否可以签到
			  map:false,//获取数据后再渲染地图，解决marker不出现问题
			  latitude:'', //经度
			  longitude:'', //纬度
			  distence:"",//距离目的地的距离
			  covers: [{
				latitude: '',//纬度
				longitude: '',//经度
				iconPath: '../../static/location.png',	//显示的图标		
				width: 30,//标记图标宽度
				height: 30,//标记图标高度
				title:'当前位置',//标注点名
				label:{//为标记点旁边增加标签
					// content:'',//文本
					// color:'#F76350',//文本颜色
					// anchorX:0,//label的坐标，原点是 marker 对应的经纬度
					// anchorY:-80,//label的坐标，原点是 marker 对应的经纬度 
					// bgColor:'#fff',//背景色
					// padding:5,//文本边缘留白
					// borderWidth:1,//边框宽度
					// borderColor:'#D84C29',//边框颜色							
					// textAlign:'right'//文本对齐方式。
				 },
				 callout:{//自定义标记点上方的气泡窗口 点击有效
						content:'地点1',
						color:'#F76350',
						fontSize:12,
						borderRadius:5,
				 }
			}]
			}
		},
		onLoad() {
			let _this = this
			uni.getLocation({
			    type: 'gcj02', //返回可以用于uni.openLocation的经纬度
			    success: function (res) {
					_this.isTrue = false
					 _this.latitude = res.latitude //当前位置经度
					 _this.longitude = res.longitude //当前位置纬度
					 _this.covers[0].latitude = res.latitude
					 _this.covers[0].longitude = res.longitude
					 // console.log(_this.covers)
					 // 计算距离目的地的距离
					 var lat1 = '22.5487160000' //目的地经度，可更改
					 var long1 = '113.8827530000' //目的地纬度，可更改
					 var radLat1 = _this.latitude * Math.PI / 180.0;
					var radLat2 = lat1 * Math.PI / 180.0;
					var a = radLat1 - radLat2;
					var b = _this.longitude * Math.PI / 180.0 - long1 * Math.PI / 180.0;
					_this.distence = 2 * Math.asin(Math.sqrt(Math.pow(Math.sin(a / 2), 2) + Math.cos(radLat1) * Math.cos(radLat2) * Math.pow(Math.sin(b / 2), 2)));
					_this.distence = _this.distence * 6378137.0; // 取WGS84标准参考椭球中的地球长半径(单位:m)
					_this.distence = Math.round(_this.distence * 10000) / 10000;
					if(_this.distence > 1000){
						uni.showToast({
							icon: "none",
							title: '您不在签到范围内',
							duration: 2000
						})
						_this.isTrue = true
					}
					 _this.map = true
					 console.log(_this.isTrue)
					// console.log(_this.distence)
					//渲染当前位置地图
			        // uni.openLocation({
			        //     latitude: _this.latitude,
			        //     longitude: _this.longitude,
			        //     success: function () {
			        //         // console.log('success');
			        //     }
			        // });
					// var map = uni.createMapContext('map');
					// map.moveToLocation();
			    },
			})
		},
		methods: {
		
		}
	}
</script>

<style>
	.map_style{
		width: 100%;
		height: 85vh;
	}
	.foot {
	    width: 100%;
	    height: 90px;
	    position: fixed;
	    bottom: 0;
	    left: 0;
	}
	
	#button {
	    width: calc(100% - 20px);
	    height: calc(100% - 40px);
	    padding: 10px;
	    margin: 10px;
	    background-color: #295dca;
		color: white;
	    border: none;
	    border-radius: 30px;
	    line-height: 30px;
	    font-size: large;
	    font-family: "楷体", serif;
	}
	
	#label {
	    margin: 10px;
	}
</style>
