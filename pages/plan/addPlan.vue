<template>
	<view>
		<view class="planType">
			<text :style="{background:selectBoolen==0?selectBg:bg}" @click="selectFunLeft">以天，时，分的计划</text>
			<text :style="{background:selectBoolen==1?selectBg:bg}" @click="selectFunRight">以年，月，日的计划</text>
		</view>
		<view class="tsfPlan" v-show="selectBoolen?0:1">
			<uni-card title="添加计划" thumbnail="" extra="额外信息" note="Tips">
				<PopCenter></PopCenter>
				<button type="default" size="mini" @click="openPop">添加</button>
			</uni-card>
		</view>
	</view>
</template>

<script>
	import PopCenter from "../plan/popCenter.vue";
	export default {
		components:{
			PopCenter,
		},
		data() {
			return {
				bg: "#ccc",
				selectBg: "red",
				selectBoolen: 0,
			}
		},
		methods: {
			selectFunLeft(){
				if(this.selectBoolen == 1){
					this.selectBoolen = 0
				}
			},
			selectFunRight(){
				if(this.selectBoolen == 0){
					this.selectBoolen = 1
				}
			},
			openPop(){
				//打开弹窗
				// this.$refs.popup.open();
			}
		}
	}
</script>

<style>
	.planType{
		width: 100%;
		height: 80rpx;
	}
	.planType text{
		display: inline-block;
		width: 50%;
		height: 100%;
		text-align: center;
		line-height: 80rpx;
	}
</style>
