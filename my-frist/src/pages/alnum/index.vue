<template>
<view>
	<view class="album_bgimg">
		<image mode="aspectFill" :src="album.cover"></image>
		<view class="album_info">
			<view class="album_name">{{album.name}}</view>
			<view class="album_btn">关注专辑</view>
		</view>
	</view>

    <view class="album_author">
		<view class="album_author_info">
			<image mode="widthFix" :src="album.user.avatar"></image>
			<view class="album_name">{{album.user.name}}</view>
		</view>
		<view class="album_author_desc"><text>{{album.desc}}</text></view>
	</view>
	
	<view class="album_images">
		<view class="album_item"
		v-for="(item,index) in wallpaper"
		:key="item.id" >
		<go-detail :list="wallpaper" :index="index">
		<image mode="aspectFill" :src="item.thumb+item.rule.replace('$<Height>',360)"></image>
		</go-detail>
		</view>
	</view>
</view>

</template>

<script>
	import goDetail from "@/components/goDetail";
	export default {
		components:{
			goDetail
		},
	 data(){
		 return{
			 params:{
				 limit:15,
				 skip:0,
				 order:"new",
				 first:1
			 },
			id:-1,
			album:{},
			wallpaper:[],
			hasmore:true
		 }
	 },
     onLoad(options) {
		this.id=options.id;
		this.getdetaillist();
     },
	 onReachBottom(){
		 if(this.hasmore){
			 this.params.skip+=this.params.limit;
			 this.getdetaillist();
			 this.params.first=0;
		 }
		 else
		 {
			 uni.showToast({
			 	title:"没有更多数据了",
				icon:"none"
			 })
		 }
	 },
	 methods:{
		 getdetaillist(){
			 this.request({
				 url:`http://157.122.54.189:9088/image/v1/wallpaper/album/${this.id}/wallpaper`,
				 data:this.params
			 }).then(result=>{
				 if(Object.keys(this.album).length===0){
				 this.album=result.res.album;
				 }
				 if(result.res.wallpaper.length===0)
				 {
					 this.hasmore=false;
					 uni.showToast({
					 	title:"没有更多数据了",
					 	icon:"none"
					 })
					 return;
				 }
				 this.wallpaper=[...this.wallpaper,...result.res.wallpaper];
			 })
		 }
	 },
	 mounted(){
		 uni.setNavigationBarTitle({title:"专辑详情"})
	 },
	}
</script>

<style lang="scss" scoped>
.album_bgimg{
	position: relative;
	.album_bgimg{
		image{
			width: 100%;
			height:200rpx;
		}
	}
	.album_info{
		position: absolute;
		width: 100%;
		left: 0;
		bottom: 0;
		display: flex;
		justify-content: space-between;
		height: 80rpx;
		align-items: center;
		color: #fff;
		padding: 0 15rpx;
		.album_name{
			font-size: 30rpx;
		}
		.album_btn{
			background-color:#d52a7e;
			width: 152rpx;
			height: 50rpx;
			display: flex;
			justify-content: center;
			align-items: center;
			border-radius: 10rpx;
		}
	}
}
.album_author{
	padding: 10rpx;
	.album_author_info{
		padding: 10rpx 0;
		display: flex;
		image{
			height: 50rpx;
			width: 50rpx;
		}
		.album_name{
			color: #000;
			margin-left: 15rpx;
		}
	}
	.album_author_desc{}
}
.album_images{
	display: flex;
	flex-wrap: wrap;
	.album_item{
		width: 33.3%;
		border: 3rpx solid #fff;
		image{
			width: 100%;
			height: 170rpx;
		}
	}
}
</style>
