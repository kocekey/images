<template>
<view>
	<view class="user_info">
		<view class="user_icon">
			<image :src="imgDetail.user.avatar" mode="widthFix"></image>
		</view>
		<view class="user_desc">
			<view class="user_name">{{imgDetail.user.name}}</view>
			<view class="user_atime">{{imgDetail.cnTime}}</view>
		</view>
	</view>
	
	<view class="high_img">
		<swiper-action @swiperAction="handleSwiperAction">
		<image mode="widthFix" :src="imgDetail.newThumb"></image>
	    </swiper-action>
	</view>
	
	<view class="user_rank">
		<view class="rank">
			<text class="iconfont icondianzan2"></text>
			<text>{{imgDetail.rank}}</text>
		</view>
		<view class="user_collect">
			<text class="iconfont iconshoucang2"></text>
			<text>收藏</text>
		</view>
	</view>

    <view class="loading_img">
		<button class="img_button" @click="handleDownload">下载图片</button>
	</view>
</view>		
</template>

<script>
	import moment from "moment";
	import swiperAction from "../../components/swiperAction";
	moment.locale("zh-cn");
	export default{
		components:{
			swiperAction
		},
		methods:{
			getdata(){
				this.album=this.imgDetail.album;
				const {imgList}=getApp().globalData;
				this.imgDetail=imgList[this.imgIndex];
				console.log(this.imgDetail);
				this.imgDetail.newThumb=this.imgDetail.thumb;
				this.imgDetail.cnTime=moment(this.imgDetail.atime*1000).fromNow();
			},
		async handleDownload(){
			await uni.showLoading({
				title:"下载中..."
			})
			
				const result1=await uni.downloadFile({url:this.imgDetail.img});
				const {tempFilePath}=result1[1];
				const result2= await uni.saveImageToPhotosAlbum({
					filePath:tempFilePath
				});
			await uni.hideLoading();
				await uni.showToast({
					title:"下载成功了"
				})
			},
			handleSwiperAction(e){
				const {imgList}=getApp().globalData;
				if(e.direction==="left" && this.imgIndex<imgList.length -1){
					this.imgIndex++;
					this.getdata();
				}else if(e.direction==="right" && this.imgIndex>0){
					this.imgIndex--;
					this.getdata();
				}else{
					uni.showToast({
						title:"没有数据了",
						icon:"none"
					})
				}
			}
		},
		data(){
			return {
				imgDetail:{},
				imgIndex:0
			}
		},
		onLoad() {
			const {imgIndex}=getApp().globalData;
			
			this.imgIndex=imgIndex;
			this.getdata();
			
		},
	}
</script>

<style lang="scss" scoped>
.user_info{
	display: flex;
	padding: 30rpx 20rpx;
	.user_icon{
		padding: 0 20rpx;
		image{
			width: 88rpx;
			border-radius: 50%;
		}
	}
	.user_desc{
		.user_name{
			color: #000;
			font-weight: 600;
		}
		.user_atime{
			color: #ccc;
			font-size: 24rpx;
			padding: 10rpx 0;
		}
	}
}

.user_rank{
	display: flex;
	padding: 15rpx 0;
	border-bottom: 1px solid #eee;
	.rank{
		flex: 1;
		display: flex;
		justify-content: center;
		align-items: center;
		.iconfont{
			margin-right: 10rpx;
		}
	}
	.user_collect{
		flex: 1;
		display: flex;
		justify-content: center;
		align-items: center;
		.iconfont{
			margin-right: 10rpx;
		}
	}
}
.loading_img{
	margin-top: 20rpx;
	.img_button{
		background-color: #d52a7e;
		color: #fff;
		font-size: 40rpx;
		}
}
</style>
