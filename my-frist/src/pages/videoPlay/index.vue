<template>
	<view class="video_play">
		<image :src="videoObj.img"></image>
		<view class="video_tool">
			<view @click="handleMuted" :class="['iconfont',muted?'iconjingyin':'iconshengyinyinliangmianxing']"></view>
			<view class="iconfont iconforward">
				<button open-type="share"></button>
			</view>
		</view>
		
		<view class="video_wrap">
             <video :muted="muted" :src="videoObj.video" objectFit="fill"></video>			
		</view>
		
		<view class="download">
			<view @click="handleDownload" class="download_btn">下载高清</view>
		</view>
		
	</view>
</template>

<script>
	export default{
		data() {
			return {
				videoObj:{},
				muted:false
			}
		},
		onLoad() {
			this.videoObj=getApp().globalData.video;
		},
		methods:{
			handleMuted(){
				this.muted=!this.muted;
			},
		async handleDownload(){
			await uni.showLoading({
				title:"下载中.."
			})
		const {tempFilePath}=(await uni.downloadFile({url:this.videoObj.video}))[1];
		await uni.saveVideoToPhotosAlbum({
			filePath:tempFilePath
		});
		uni.hideLoading();
		uni.showToast({
			title:"下载成功！"
		})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.video_play{
		position: relative;
		height: 100vh;
		image{
			position: absolute;
			width: 100%;
			height: 100%;
			z-index: -1;
			filter: blur(10px);
			}
		.video_tool{
			height: 80rpx;
			display: flex;
			justify-content: flex-end;
			.iconfont{
			width: 80rpx;
			color: #fff;
			font-size: 50rpx;
			border-radius: 40rpx;
			background-color: rgba(0,0,0,0.3);
			display: flex;
			justify-content:center;
			align-items: center;
			margin-right: 20rpx;
			}
			.iconforward{
				position: relative;
				button{
					position: absolute;
					width: 100%;
					height: 100%;
					opacity: 0;
				}
			}
		}
		.video_wrap{
			display: flex;
			justify-content: center;
			video{
				width: 360rpx;
				height: 600rpx;
			}
		}
		.download{
			display: flex;
			justify-content: center;
			margin-top: 30rpx;
			.download_btn{
				width: 360rpx;
				height: 40rpx;
				border-radius: 40rpx;
				display: flex;
				justify-content: center;
				align-items: center;
				color: #fff;
				border: 1px solid #fff;
				
				background-color: #666;
			}
		}
	}
</style>
