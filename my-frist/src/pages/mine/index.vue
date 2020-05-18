<template>
	
 <view>
	 
	<view class="photo"><text class="iconfont iconzhaoxiang"></text></view> 
	
	<view class="title">
		<view class="header"><image mode="widthFix" src="../../static/images/my.png"></image></view>
		<view class="info">
			<view class="info_name">17</view>
			<view class="info_right">
				<view class="info_ID">微信号:kocekey17</view>
				<view class="info_erwei">
					<text class="iconfont iconico"></text>
					<text class="iconfont iconiconfontxiangxia1copy19"></text>
				</view>
			</view>
		</view>
	</view> 
	
	<view class="payfor">
		<text class="iconfont iconzhifu"></text>
		<text class="font">支付</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
	<view class="tubiao">
		<text class="iconfont iconshoucangdianjihou"></text>
		<text class="font">收藏</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
	<view class="tubiao">
		<text class="iconfont iconxiangce"></text>
		<text class="font">相册</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
	<view class="tubiao">
		<text class="iconfont iconqiabao"></text>
		<text class="font">卡包</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
	<view class="smile">
		<text class="iconfont iconbiaoqing"></text>
		<text class="font">表情</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
	<view class="tubiao">
		<text class="iconfont iconshezhi"></text>
		<text class="font">设置</text>
		<text class="iconfont iconiconfontxiangxia1copy19"></text>
	</view>
	
 </view>
 
</template>

<script>
export default {
}
</script>

<style lang="scss" scoped>
	
 .photo{
	 width: 100vw;
	 display: flex;
	 justify-content: flex-end;
	 .iconzhaoxiang{
		 padding: 20rpx 30rpx;
		 font-size: 50rpx;
	 }
 }
.title{
	display: flex;
	flex-wrap: nowrap;
	padding: 0rpx 0rpx 60rpx 0rpx;
	border-bottom: 20rpx solid #EDEDED;
	.header{ 
		image{
			width: 150rpx;
			height: 150rpx;
		}
	}	
	.info{
		margin-left: 10rpx;
		height: 130rpx;
		display: flex;
		flex-wrap: wrap;
		align-content: space-between;
		.info_name{
			font-size: 45rpx;
			font-weight: 600;
			color: #000;
			width: calc(100vw - 170rpx);
		}
		.info_right{
			width: calc(100vw - 170rpx);
			display: flex;
			flex-wrap: nowrap;
			justify-content: center;
			align-items: center;
			.info_ID{
				flex: 8;
			}
			.info_erwei{
				flex: 1;
				display: flex;
				justify-content: center;
				align-items: center;
				.iconico{
					margin-right: 30rpx;
					font-size: 35rpx;
				}
				.iconiconfontxiangxia1copy19{
					margin-right: 10rpx;
				}
			}
		}
	}
}
.payfor{
	width: 100vw;
	display: flex;
	padding: 30rpx;
	border-bottom: 20rpx solid #EDEDED;
	justify-content:space-between;
	justify-content: center;
	align-items: center;
	.iconzhifu{
		margin-right: 20rpx;
	}
	.font{
		flex: 1;
	}
	.iconiconfontxiangxia1copy19{
		margin-right: -10rpx;
	}
}
.tubiao{
	width: 100vw;
	display: flex;
	padding: 30rpx;
	border: 1rpx solid #F1F1F1;
	justify-content:space-between;
	justify-content: center;
	align-items: center;
	.iconshoucangdianjihou{
		margin-right: 20rpx;
	}
	.font{
		flex: 1;
	}
	.iconiconfontxiangxia1copy19{
		margin-right: -10rpx;
	}
}
.iconxiangce{margin-right: 20rpx;}
.iconqiabao{margin-right: 20rpx;}
.iconshezhi{margin-right: 20rpx;}
.smile{
	width: 100vw;
	display: flex;
	padding: 30rpx;
	border-bottom: 20rpx solid #EDEDED;
	justify-content:space-between;
	justify-content: center;
	align-items: center;
	.iconbiaoqing{
		margin-right: 20rpx;
	}
	.font{
		flex: 1;
	}
	.iconiconfontxiangxia1copy19{
		margin-right: -10rpx;
	}
}
</style>