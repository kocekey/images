<template>
	<view>
		
	<scroll-view @scrolltolower="handleScrollToLower" scroll-y enable-flex class="video_main">
		<view class="video_item" v-for="item in videowp" :key="item.id" @click="handleGoVideo(item)">
			<image mode="widthFix" :src="item.img"></image>
		</view>
	</scroll-view>
	
	</view>
</template>

<script>
	export default{
		data(){
			return{
				videowp:[],
				hasmore:true
			}
		},
		props:{
			urlobj:Object
		},
		watch:{
			urlobj(){
				this.videowp=[];
				this.getList();
			}
		},
		mounted(){
			this.getList();
		},
		methods:{
			handleGoVideo(item){
				getApp().globalData.video=item;
				uni.navigateTo({
					url:"/pages/videoPlay/index"
				})
			},
			handleScrollToLower(){
				if(this.hasmore){
					this.urlobj.skip+=this.urlobj.params.limit;
					this.getList();
				}else{
					uni.showToast({
						title:"没有更多数据了",icon:"none"
					})
				}
			},
			getList(){
				this.request({
					url:this.urlobj.url,
					data:this.urlobj.params
				}).then(result=>{
					if(result.res.videowp.length ===0){
						this.hasmore=false;
						uni.showToast({
							title:"没有更多数据了",icon:"none"
						});
						return;
					}
					this.videowp=[...this.videowp,...result.res.videowp];
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.video_main{
		display: flex;
		flex-wrap: wrap;
        height: calc(100vh - 36px);
		.video_item{
			width: 33.3%;
			border: 5rpx solid #fff;
		}
	}
</style>
