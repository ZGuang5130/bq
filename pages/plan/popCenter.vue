<template>
	<view>
		<view class="mask" :style="{width:maskWidth,height:maskHeight,background:'red',opacity:'0.5'}">
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				maskWidth: this.phoneWidth,
				maskHeight: this.phoneHeight
			}
		},
		created() {
			console.log(this)
		},
		methods: {
			
		}
	}
</script>

<style>
	.mask{
		position: fixed;
		top: 0;
		left: 0;
	}
</style>
