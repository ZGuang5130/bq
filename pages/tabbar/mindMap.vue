<template>
	<view>
		<view class="">
			<view class="search">
				<input type="text" value="" placeholder="添加好友/搜索好友" />
				<image src="../../static/ming-pop/close.png" mode=""></image>
			</view>
			<view class="friend">
				<view class="">
					<text>我的好友</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	.search{
		width: 100%;
		height: 60px;
		background: #CCCCCC;
		position: relative;
	}
	.search input{
		width: 90%;
		height: 40rpx;
		background-color: #fff;
		position: absolute;
		top: 20px;
		left: 5%;
	}
	.search image{
		width: 10px;
		height: 10px;
		position: absolute;
		top: 25px;
		right: 25px;
	}
</style>
