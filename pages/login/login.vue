<template>
	<view>
		<view class="signIn" :style="{height:signInHeight}">
			<view class="signInContent">
				<view class="" style="margin: 120rpx 4rpx;">
					<text style="color: yellow;">每天进步一点点</text>
				</view>
				<view class="clearfix" style="margin: 100rpx 0rpx;height: 60rpx;">
					<text style="float: left;">用&nbsp;&nbsp;户&nbsp;&nbsp;名：</text><input style="float: left;" v-model="userName" type="text" value="" />
				</view>
				<view class="clearfix" style="margin: 100rpx 0rpx;height: 60rpx;">
					<text style="float: left;">密&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;码：</text><input style="float: left;" v-model="passWord" type="password" value="" />
				</view>
				<view class="clearfix" style="margin: 60rpx 0rpx;height: 60rpx;" v-show="zc">
					<text style="float: left;">确认密码：</text><input style="float: left;" v-model="againPassWord" type="password" value="" />
				</view>
			</view>
			<view class="signInButton" style="margin-top: 120rpx;" >
				<view class="" v-show="zc?false:true">
					<button type="default" @click="register">注册</button>
					<button type="default" @click="login">登入</button>
				</view>				
				<view class="" v-show="zc">
					<button type="default" @click="determine">确定</button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				userName: "",
				passWord: "",
				againPassWord: "",
				signInHeight: document.body.clientHeight + 'px',
				zc: false,
			}
		},
		onLoad: function (option) {
			if(option.id == 1){
				this.zc = true
			}
		},
		methods: {		
			register(){
				this.zc = true
			},
			login(){
				if(this.userName == "admin"){
					if(this.passWord === "admin"){
						uni.reLaunch({
							url:'../index/index'
						})
					}else{
						alert('账号密码不对')
					}
				}else{
					alert('账号密码不对')
				}
			},
			determine(){
				if(this.passWord === this.againPassWord){
					uni.reLaunch({
						url:"../index/index"
					})
				}else{
					alert("密码不一致")
				}
			}
		}
	}
</script>

<style>
.signIn{
	width: 100%;
	background-image: url(../../static/drbj.jpg);
	opacity: 0.8;
}
.signInContent{
	width: 80%;
	margin: 0 auto;
	text-align: center;
	padding-top: 30%;
	font-size: 40rpx;
	color: #00F5FF;
	/* background-color: linear-gradient(to right, red , yellow); */ 
}
.signInContent input{
	display: inline-block;
	text-align: left;
	border: 1px solid #DBB304;
	background-image: linear-gradient(to right, #ff9569 0%, #e92758 100%);
	height: 30px;
	margin-left: 20rpx;
}
.signInButton{
	width: 80%;
	margin: 0 auto;
	text-align: center;
}
.signInButton button{
	background-image: linear-gradient(-90deg, #29bdd9 0%, #276ace 100%);
	margin: 40rpx 10rpx;
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
</style>
