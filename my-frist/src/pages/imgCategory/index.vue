<template>

	<view>
        <view class="category_tab">
			<view class="category_tab_title">
				<view class="title_inner">
					<uni-segmented-control
					:values="item.map(v=>v.title)"
					:current="currtent"
					@clickItem="onClickItem"
					style-type="text"
					active-color="#d4237a"
					>
					</uni-segmented-control>
				</view>
				<view class="iconfont iconsearch"></view>
			</view>
			<scroll-view enable-flex scroll-y class="category_tab_content" @scrolltolower="handleToLower">
				<view class="cate_item" v-for="(item,index) in vertical" :key="item.id">
				 <go-detail :list="vertical" :index="index">
					<image :src="item.thumb" mode="widthFix"></image>
				</go-detail>
				</view>
			</scroll-view>
		</view>	
	</view>

</template>

<script>
	import{uniSegmentedControl} from "@dcloudio/uni-ui";
	import goDetail from "@/components/goDetail";
	export default{
		components:{
			uniSegmentedControl,
			goDetail
		},
		data() {
			return {
				item:[{title:"最新",order:"new"},{title:"热门",order:"hot"}],
					current:0,
					params:{limit:30,skip:0,order:"new"},
					id:0,
					vertical:[],
					hasmore:true
			};
		},
		methods:{
			handleToLower(){
				if(this.hasmore){
					this.params.skip+=this.params.limit;
					this.getList();
				}else{
					uni.showToast({
						title:"没有更多数据了",
						icon:"none"
					})
				}
			},
			onClickItem(e){
			if(this.current!==e.currentIndex){
				this.current=e.currentIndex;
			   }else{return;}
			   this.params.order=this.item[e.currentIndex].order;
			   this.params.skip=0;
			   this.vertical=[];
			   this.getList();
		   },
		   getList(){
			   this.request({
				   url:`http://157.122.54.189:9088/image/v1/vertical/category/${this.id}/vertical`,
				   data:this.params
			   }).then(result=>{
				   if(result.res.vertical.length===0){
					   this.hasmore=false;
					   uni.showToast({
					   	title:"没有更多数据了",
						icon:"none"
					   })
					   return;
				   }
				   this.vertical=[...this.vertical,...result.res.vertical];
			   })
		   }
		},
		onLoad(options) {
			this.id=options.id;
			this.getList();
		}
	}
</script>

<style lang="scss" scoped>
	.category_tab{
		.category_tab_title{
			position: relative;
			.title_inner{
				width: 60%;
				margin: 0 auto;
			}
			.iconsearch{
				position: absolute;
				top: 50%;
				transform: translateY(-50%);
				right: 5%;
			}
		}
		.category_tab_content{
			display: flex;
			flex-wrap: wrap;
			height: calc(100vh - 36px);
			.cate_item{
				width: 33.3%;
				border: 5rpx solid #fff;
				image{
					
				}
			}
		}
	}
</style>
