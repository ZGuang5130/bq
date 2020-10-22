<template>
	<view>
		<view class="mask" :style="{width:maskWidth,height:maskHeight,background:'#222222',opacity:'0.5'}">			
		</view>
		<view class="addpaln">
			<text style="color: #FFFFFF;">添加计划</text>
			<input type="text" value="" />
			<input type="text" value="" />
			<button type="default" size="mini" @click="add">确定</button>
			<button type="default" size="mini" @click="cancel">取消</button>
		</view>			
	</view>
</template>

<script>
	export default {
		data() {
			return {
				maskWidth: document.body.clientWidth + 'px',
				maskHeight: document.body.clientHeight + 'px'
			}
		},
		created() {
			
		},
		methods: {
			add(){
				
			},
			cancel(){
				console.log(this)
				this.popShow == 1
			}
		}
	}
</script>

<style>
	.mask{
		position: fixed;
		top: 0;
		left: 0;
		z-index: 100;
	}
	.addpaln{
		position: fixed;
		top: 20%;
		left: 0;
		z-index: 101;
	}
</style>
