<template>
	<view class="Login_bk">
		<view class="title"><text>欢迎来到邮签</text></view>
		<button type="primary" @click="start()">开启邮签之旅</button>
		<text style="margin-top:10rpx">一键登录您的账号并绑定学号</text>
		<text style="position:absolute;bottom:10rpx">(该过程会跳转到信息门户验证您的身份)</text>
	</view>
	
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			start(){
				const app=getApp()
				if(app.globalData.isLogin===0){
					uni.navigateTo({
						url:'../out/out'
					})
				}
				else{
					uni.reLaunch({
						url:'../index/index'
					})
			}
			}
		}
	}
</script>

<style>
	/* pages/login/login.wxss */
	.Login_bk{
	  width: 100vw;
	  height: 100vh;
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	}
	.title{
	  margin-top: 100rpx;
	  margin-bottom: 400rpx;
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  align-items: center;
	  font-size: 40px;
	  font-weight: bold;
	}
</style>
