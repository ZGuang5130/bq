<template>
	<view>
		<view class="content">
			<view class="hearder" style="text-align: center;background-color: orange;height: 90rpx;line-height: 2.7;color: red;">
				{{realdate}}
			</view>
			<uni-card title="每天必做的事" thumbnail="" :extra="nowDate" note="Tips">
				<checkbox-group name="mustDo">		
						<label class="checkbox" @tap="radioChange(mustDoList.id)" v-for="(mustDoList,index) in mustDoLists" :key="index">
							<checkbox style="display: inline-block;transform:scale(0.6)" :checked="mustDoList.current == 1" value="mustDoList.id" />
							<text class="bqindex">{{index+1}}.</text>
							<text :class="{accomplishText:mustDoList.current}" class="mustDoContent" :style="{color:mustDoList.selectColor}">{{mustDoList.mustDoText}}</text>
							<text class="mustDoDate">{{mustDoList.startDate}}</text><text>-</text><text class="">{{mustDoList.endDate}}</text>
						</label>
				</checkbox-group>
			</uni-card>
			<uni-card title="现在要做的事" thumbnail="" :extra="nowTime" note="Tips">	
				<view class="" :style="{color:mustDoDate.color}">
					{{mustDoDate.mustDoText}}
				</view>
				<view class="">
					<swiper :indicator-dots="false" :autoplay="true" :interval="5000" :duration="2000" style="min-height: 500rpx;">
						<swiper-item>
							<view class="swiper-item">
								<image src="../../static/now1.jpg" mode="" style="border: 1px solid #ccc;"></image>
							</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item">
								<image src="../../static/now1.jpg" mode="" style="border: 1px solid #ccc;"></image>
							</view>
						</swiper-item>
					</swiper>
				</view>
				
			</uni-card>
		</view>
		<view class="planButton">
			<button type="default" size="mini" @click="addPlan">添加计划</button>
			<button type="default" size="mini">修改计划</button>	
		</view>
	</view>
</template>

<script>
	/**
	 * 修改uni-card组件中，title的颜色变化。note的颜色变化。extra的颜色变化。修改组件。
	 */
	export default {
		data() {
			return {
				mustDoDate:{},
				nowDate: "",
				nowTime: "",
				realdate: "",
				sortDate: "",
				timer: "",
				mustDoLists:[
					{	
						id:1,
						startDate: "08:20",
						endDate: "09:00",
						mustDoNum:"1",
						mustDoText:"修改组件的高度，固定高，设置可以滚动，右侧不显示滚动条。",
						current: 0,
						color: "",
						selectColor: "",
						img: [],      //添加图片路径，组成数组，3张图片
					},
					{
						id:2,
						startDate: "16:00",
						endDate: "15:20",
						mustDoNum:"2",
						mustDoText:"优化 修改代码。",
						current: 0,
						color: "",
						selectColor: "",
						img: [],
					},
					{
						id:3,
						startDate: "14:20",
						endDate: "15:20",
						mustDoNum:"3",
						mustDoText:"继续编写代码，每天编写一页.",
						current: 0,
						color: "",
						selectColor: "",
						img: [],
					},
					{
						id:4,
						startDate: "13:20",
						endDate: "14:20",
						mustDoNum:"4",
						mustDoText:"思考项目架构，记录数据",
						current: 0,
						color: "",
						selectColor: "",
						img: [],
					}
				]
			}
		},
		created() {
			//现在必须做的事，实时更新时间，进行页面数据更新。
			this.timer = setInterval(this.realTime,1000)	
			
		},
		mounted() {
			//处理时间排序sort
			this.sortMustDoDate()
			
		},
		methods: {
			// 后续把时间写成组件，并且实时更新，可以读秒。
			realTime() {
				const newDate = new Date();
				const y = newDate.getFullYear();
				const m = newDate.getMonth() + 1;
				this.m = m < 10 ? ('0' + m) : m;
				const d = newDate.getDate();
				this.d = d < 10 ? ('0' + d) : d;
				const h = newDate.getHours();
				this.h = h < 10 ? ('0' + h) : h;
				const minute = newDate.getMinutes();
				this.minute = minute < 10 ? ('0' + minute) : minute;
				const s = newDate.getSeconds();
				this.s = s < 10 ? ('0' + s) : s;
				const xq = "星期" + "日一二三四五六".charAt(newDate.getDay());
				this.realdate =  y + '年' + this.m + '月' + this.d + '日'+ ' ' + this.h + ':' + this.minute +':' + this.s + ' ' + xq;
				this.nowDate = y + '-' + this.m + '-' + this.d;
				this.nowTime = this.h + ':' + this.minute +':' + this.s;
				this.sortDate = this.h + ':' + this.minute;
				
			},
			// 代码很low，后期优化
			radioChange(id) {
				for(let i=0;i<this.mustDoLists.length;i++){
					if(this.mustDoLists[i].id == id){
						if(this.mustDoLists[i].current == 0){
							this.mustDoLists[i].current = 1
						}else{
							this.mustDoLists[i].current = 0
						}
					}
				}
			},
			//显示正在做的事。实时更新。
			sortNowDate(){
				for(let i=0;i<this.mustDoLists.length;i++){
					if(this.mustDoLists[i].endDate>this.sortDate && this.sortDate>this.mustDoLists[i].startDate){
						this.mustDoDate = this.mustDoLists[i]
						this.mustDoDate.color = "blue"
						this.mustDoLists[i].selectColor = "red"
					}
				}
			},
			// 时间排序，比较时间顺序，修改时间后，修改顺序。后续添加重要性排序。
			sortMustDoDate(){
				let mdlt = this.mustDoLists
				let numArr = []
				for(let i=0;i<mdlt.length;i++){
					numArr.push(mdlt[i].startDate)
				}
				numArr.sort()
				for(let n=0;n<numArr.length;n++){
					for(let m=0;m<mdlt.length;m++){
						if(numArr[n] == mdlt[m].startDate){
							this.swapArr(mdlt,n,m)
						}
					}
				}					
			},
			//数组两个元素调换位置
			swapArr(arr, index1, index2) {
			    arr[index1] = arr.splice(index2, 1, arr[index1])[0];
			    return arr;
			},
			//向上一格
			upGo(arr,index){			 
			    if(index!=0){			 
			        arr[index] = arr.splice(index-1, 1, arr[index])[0];			 
			    }else{			 
			        arr.push(arr.shift());			 
			    }			 
			},
			//向下一格
			downGo(arr,index) {			 
			    if(index!=arr.length-1){			 
					arr[index] = arr.splice(index+1, 1, arr[index])[0];		 
			    }else{			 
			        arr.unshift( arr.splice(index,1)[0]);			 
			    }			 
			},
			addPlan(){
				uni.navigateTo({
					url: "../plan/addPlan",
				})
			}
		},
		updated() {
			this.sortNowDate()
		},
		beforeDestroy() {
			if(this.timer){
				clearInterval(this.timer)
			}
		}
	}
</script>

<style>
	[contenteditable="true"]:focus {
		outline: #FFFFFF;
	}
	text{
		display: inline-block;
		font-size: 24rpx; 
		padding-left: 20rpx;		
	}
	.mustDoDate{
		padding-left: 40rpx;
	}
	.mustDoContent{
		width: 50%;
		overflow: hidden;
		text-overflow: ellipsis;	
		white-space: nowrap;
		line-height: 1;
	}
	.bqindex{
		font-weight: 700;
		color: red;
		font-size: 28rpx;
		padding-left: 0;
	}
	.accomplishText{
		text-decoration: line-through;
		text-decoration-color: green;
		text-decoration-style: wavy;
		color: #C0C0C0;
	}
	.incompleteText{
		text-decoration: none;
	}
	.clearfix:after{/*伪元素是行内元素 正常浏览器清除浮动方法*/
		content: "";
		display: block;
		height: 0;
		clear:both;
		visibility: hidden;
	}
	.clearfix{
	    *zoom: 1;/*ie6清除浮动的方式 *号只有IE6-IE7执行，其他浏览器不执行*/
	}
	.planButton{
		text-align: center;
	}
	button{
		width: 200rpx;
		height: 60rpx;
		margin-left: 10rpx;
	}
</style>
