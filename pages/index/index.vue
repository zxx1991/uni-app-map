<template>
	<view class="content">
		<view class="header">
			<text class="title">太和镇-镇北下册村</text>
			<!-- <p class="header_right">
				<image class="search" @click="toMap" src="../../static/search.png"></image>
				<image class="share" src="../../static/share.png"></image>
			</p> -->
		</view>
		
		<!-- <view class="button_line_top">
			<!-- <span class="button_style">村居简介</span> -->
			<!-- <span class="button_style red_color" @click="toMap" >签到</span> -->
			<!-- <span class="button_style red_color">导航</span> -->
		<!-- </view> --> 
		
		<view class="content_text">
			<text>北下册村在淄川区政府驻地东南18.6千米处，属太河镇管辖。东跨淄河至东下册村，西至...北下册村在淄川区政府驻地东南18.6千米处，属太河镇管辖。东跨淄河至东下册村，西至...北下册村在淄川区政府驻地东南18.6千米处，属太河镇管辖。东跨淄河至东下册村，西至...北下册村在淄川区政府驻地东南18.6千米处，属太河镇管辖。东跨淄河至东下册村，西至...北下册村在淄川区政府驻地东南18.6千米处，属太河镇管辖。东跨淄河至东下册村，西至...</text>
		</view>
		<span class="button_style red_color" @click="toMap" >签到</span>
		<!-- <view class="button_line_down">
			<span class="button_style">村书记</span>
			<span class="button_style">村主任</span>
			<span class="button_style">村居详情</span>
		</view> -->
		
			
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {
			
		},
		methods: {
			toMap(){
				uni.redirectTo({
					url: 'pay'
				});
			}
		}
	}
</script>

<style>
	.content{
		width: 100%;
	}
	.header{
		width: 100%;
		height: 100upx;
		background: #4759BD;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.header .title{
		font-size: 40upx;
		color: #ffffff;
		line-height: 100upx;
		margin-left: 30upx;
	}
	.header .header_right{
		margin-right: 40upx;
	}
	.header .search,.header .share{
		width: 40upx;
		height: 40upx;
	}
	.header .search{
		margin-right: 60upx;
	}
	.button_line_top,.button_line_down{
		width: 80%;
		height: 60upx;
		margin: 30upx auto 0 auto;
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-top: 30upx;
	}
	.button_style{
		display: block;
		width: 80upx;
		background: #039B8C;
		line-height: 50upx;
		color: #ffffff;
		border-radius: 4upx;
		font-size: 28upx;
		padding: 0 20upx;
		text-align: center;
		margin: 40upx auto;
	}
	.red_color{
		background: #EF4681;
	}
	.content_text{
		width: 70%;
		margin: 20upx auto;
		padding-bottom: 50upx;
		border-bottom: 1px solid #F0F0F0;
		font-size: 32upx;
		line-height: 60upx;
		color: #515151;
	}
</style>
