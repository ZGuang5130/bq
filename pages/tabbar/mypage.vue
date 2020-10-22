<template>
	<view>
		<view class="mypage">
			<view class="myHerder">
				<view class="noLogin" :class='loginNum?dn:db'>
					<view class="noLoginType">
						<text @click="login">登入</text><text>/</text><text @click="register">注册</text>
					</view>
				</view>
				<view class="myMessage" :class='loginNum?db:dn'>
					<view class="headPortrait">
						<image class="userImage" :src="userHeadPortrait" mode=""></image>
						<image class="sexImage" :src="manSexSrc" mode=""></image>
					</view>
					<view class="userMessage">
						<text style="padding: 0 10px;color: #007AFF;">狗蛋</text><text style="color: #F0AD4E;">数据库拉回到家卡还是就看到</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				manSexSrc:"../../static/man.png",
				womanSexSrc:"../../static/woman.png",
				unknownSexSrc:"../../static/unknown.png",
				userHeadPortrait:"../../static/now1.jpg",
				loginNum:false,
				dn:'displayNone',
				db:'displayBlock'
			}
		},
		methods: {
			login(){
				uni.navigateTo({
					url:'../login/login?id=0'
				})
			},
			register(){
				uni.navigateTo({
					url:'../login/login?id=1'
				})
			}
		}
	}
</script>

<style>
.myHerder{
	width: 100%;
	height: 400rpx;
	background: yellow;
}
.noLoginType{
	width: 100px;
	height: 50rpx;
	text-align: center;
	position: absolute;
	top: 100rpx;
	left: 38%;
}
.displayNone{
	display: none;
}
.displayBlock{
	display: block;
}
.myMessage{
	width: 100%;
}
.headPortrait{
	width: 100px;
	height: 100px;
	margin: 0px auto;
	padding-top: 20px;
}
.headPortrait .userImage{
	width: 100px;
	height: 100px;
	border-radius: 50%;
}
.sexImage{
	width: 20px;
	height: 20px;
	border-radius: 50%;
	position: absolute;
	top: 100px;
	left: 55%;
	/* opacity: 0.5; */
}
.userMessage{
	text-align: center;
}
.userMessage text{
	font-size: 24rpx;
}
</style>
