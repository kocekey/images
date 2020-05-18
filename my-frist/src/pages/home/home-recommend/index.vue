<template>
<scroll-view @scrolltolower="handleToLower" class="recommend_all" scroll-y v-if="recommends.length>0">
  <view class="recommend_wrap">
	  
	 <navigator class="recommend_item" v-for="item in recommends" :key='item.id'>
		 <image mode="widthFix" :src="item.thumb"></image> 
	 </navigator> 
	 
	 <view class="months_wrap">
		    <view class="months_title">
			    <view class="months_title_info">
				    <view class="months_info">
					<text>{{monthes.DD}}/</text>{{monthes.MM}}月
					</view>
					<view class="months_text">{{monthes.title}}</view>
				</view>
			    <view class="months_more">更多 > </view>
			</view>
		<view class="months_content">
			<view class="months_item" v-for="(item,index) in monthes.items" :key="item.id">
				<go-detail :list="monthes.items" :index="index">
				<image 
				mode="aspectFill" 
				:src="item.thumb+item.rule.replace('$<Height>',360)">
				</image>
				</go-detail>
			</view>
		</view>
	 </view>
	 
	 <view class="hot_wrap">
		 <view class="hots_title">
			 <text>热门</text>
		 </view>
		 <view class="hots_content">
			<view class="hot_item" v-for="(item,index) in hots" :key="item.id">
			<go-detail :list="hots" :index="index">
			<image mode="widthFix" :src="item.thumb"></image>	
			</go-detail>
			</view> 
		 </view>
	 </view>
  </view>
</scroll-view>  
</template>
 
<script>
	import moment from "moment";
	import goDetail from "@/components/goDetail";
export default {
	components:{
		goDetail
	},
	data(){
		return{
			recommends:[],
			monthes:{},
			hots:[],
			params:{limit:30, order:"hot", skip:0 },
			hasmore:true
		}
	},
	methods:{
		handleToLower(){
			if(this.hasmore){
			this.params.skip+=this.params.limit;
			this.getlist()
			}
			else{
				uni.showToast({
					title:"没有数据了",
					icon:"none"
				})
			}
		},
		getlist(){
			this.request({
					   url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
					   data:this.params
			}).then(result=>{
				if(result.res.vertical.length===0)
				{
					this.hasmore=false;
					return;
				}
					   if(this.recommends.length===0)
					   {
					   this.recommends=result.res.homepage[1].items;
					   //月份
					   this.monthes=result.res.homepage[2];
					   //将时间转换为时间格式
					   this.monthes.MM=moment(this.monthes.stime).format("MM");
					   this.monthes.DD=moment(this.monthes.stime).format("DD");
					   }
					   //获取热门数据,数组拼接
					   this.hots =[...this.hots,...result.res.vertical];
			})
		}
	},
   mounted(){
	   this.getlist(),
	   uni.setNavigationBarTitle({title:"推荐"})
   }
}
</script>

<style lang="scss" scoped>
.recommend_all{
	height: calc(100vh - 36px);
}
.recommend_wrap{
	display: flex;
    flex-wrap: wrap;
	.recommend_item{
		width: 50%;
		border: 3rpx solid #fff;
	}
}
.months_wrap{
	.months_title{
		width: 100vw;
		display: flex;
		justify-content: space-between;
		padding: 15rpx;
		.months_title_info{
			color: #d52a7e;//01月的样式
			font-size: 30rpx;
			display: flex;
			align-items: center;
			.months_info{
				text{
					font-size: 36rpx;//18的样式
					font-weight: 700;
				}
			}
			.months_text{
				font-size: 34rpx;//你负责
				font-weight: 700;
				color: #666;
				margin-left: 20rpx;
			}
		}
		.months_more{
			display: flex;//更多的样式
			align-items: center;
			font-size: 28rpx;
			color: #d52a7e;
		}
	}
	.months_content{
		display: flex;
        flex-wrap: wrap;
		.months_item{
			width: 33.3%;
			border: 3rpx solid #fff;
		}
	}
}
.hot_wrap{	
	width: 100vw;
	.hots_title{
		padding: 20rpx;
			text{
				padding-left: 15rpx;
				border-left: 20rpx solid #d52a7e;
				font-size: 30rpx;
				font-weight: 700;
			}
		}
		.hots_content{
			display: flex;
			flex-wrap: wrap;
			.hot_item{
				width: 33.3%;
				border: 3rpx solid #fff;
			}
		}
}

</style>