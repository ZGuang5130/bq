<template>
	<view>
		<view class="planType">
			<text :style="{background:selectBoolen==0?selectBg:bg}" @click="selectFunLeft">以天，时，分的计划</text>
			<text :style="{background:selectBoolen==1?selectBg:bg}" @click="selectFunRight">以年，月，日的计划</text>
		</view>
		<view class="tsfPlan" v-show="selectBoolen?0:1">
			<uni-card title="添加计划" thumbnail="" extra="额外信息" note="Tips">
				<view class="planLists">
					<view class="palnList" v-show="index==0?false:true" v-for="(list,index) in addPlanLists">
						<text class="" style="padding-left: 20rpx;">{{index}}.</text>
						<text class="" style="width: 400rpx;padding-left: 10rpx;">{{list.pl}}</text>
						<text class="" style="margin-left: 40rpx;">{{list.sd}}</text><text>-</text><text class="">{{list.ed}}</text>
					</view>
				</view>
				<view v-show="popShow?0:1">
					<view class="mask" :style="{width:maskWidth,height:maskHeight,background:'#222222',opacity:'0.5'}">			
					</view>
					<view class="addpaln">
						<view class="addPlanTop">		
							<view class="" style="margin-left: 10rpx;">
								<text style="color: #FFFFFF;">添加计划:</text>
							</view>
							<view class="" style="display: inline-block;width: 100%;margin-top: 10rpx;">
								<input class="datePlan planText" style="width: 80%;" type="text" v-model="addPlanList.pl" value="" />
								<input class="datePlan planStartDate" style="width: 40rpx;" type="text" v-model="addPlanList.sd" value="" />
								<input class="datePlan planEndDate" style="width: 40rpx;" type="text" v-model="addPlanList.ed" value="" />
							</view>
						</view>					
						<view class="addPlanButton" style="margin-top: 50rpx;">
							<button type="default" size="mini" @click="add">确定</button>
							<button type="default" size="mini" @click="cancel">取消</button>
						</view>			
					</view>			
				</view>
				<view class="" style="text-align: center;margin-top: 20rpx;">
					<button class="addButton addPlanButton" type="default" size="mini" @click="openPop">添加</button>
					<button class="reviseButton addPlanButton" type="primary" size="mini" @click="openPop">修改</button>
					<button class="delButton addPlanButton" type="warn" size="mini" @click="openPop">删除</button>
				</view>
				
			</uni-card>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addPlanList:{
					pl:'',
					sd: '',
					ed: '',
				},				
				bg: "#ccc",
				selectBg: "red",
				selectBoolen: 0,
				popShow:1,
				maskWidth: document.body.clientWidth + 'px',
				maskHeight: document.body.clientHeight + 'px',
				addPlanLists:[{}]
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
				if(this.popShow == 0){
					this.popShow = 1
				}else{
					this.popShow = 0
				}
			},
			add(){
				this.addPlanLists.push(this.addPlanList)
				this.popShow = 1
			},
			cancel(){
				this.popShow = 1
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
	.mask{
		position: fixed;
		top: 0;
		left: 0;
		z-index: 100;
	}
	.addpaln{
		width: 100%;
		position: fixed;
		top: 20%;
		left: 0;
		z-index: 101;
	}
	.datePlan{
		display: inline-block;
		background: #fff;
		height: 60rpx;
		margin-left: 10rpx;
	}
	.addPlanTop{
		width: 100%;
		height: 50px;
	}
	.addPlanTop text{
		
	}
	.addPlanButton{
		width: 100%;
		text-align: center;
	}
	.palnList{
		width: 100%;
	}
	.planLists{
		width: 100%;
		min-height: 100rpx;
		border: 1px solid #ccc;
	}
	.addPlanButton{
		margin: 8rpx 8rpx;
	}
</style>
