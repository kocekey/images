<template>
	<view @click="handleClick">
		<slot></slot>
	</view>
</template>

<script>
	export default{
		props:{
			list:Array,
			index:Number
		},
		methods:{
			handleClick(){
				console.log(this.list);
				
				getApp().globalData.imgList=this.list;
				getApp().globalData.imgIndex=this.index;
				uni.navigateTo({
					url:"/pages/imgDetail/index"
				})
			}
		}
	}
</script>

<style>
</style>
