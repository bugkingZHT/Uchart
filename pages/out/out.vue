<template>
	<view class="bk">
	    <view class="cu-form-group" style="margin-top:50rpx;">
	    	<view class="title">学号</view>
	    	<input placeholder="学号" type="number" name="input" @input="getbuptID"></input>
	    </view>
	    <view class="cu-form-group" style="margin-top: 50rpx;">
	    	<view class="title">密码</view>
	    	<input placeholder="信息门户密码" name="input" type="number" password="true"></input>
	    </view>
		<view class="cu-form-group" style="margin-top: 50rpx;">
			<view class="title">昵称</view>
			<input placeholder="昵称" name="input" type="text" @input="getnickname"></input>
		</view>
			<button @click="login_bupt" type="primary" class="btn1">学号注册</button>
			<a href="" style="margin-top: 10rpx;" bindtap="login_none">暂不使用学号注册</a>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				code:'',
				buptID:'',
				inta:'',
				nickname:''
			}
		},
		methods: {
			getbuptID(event){
				this.buptID=event.detail.value;
			},
			getnickname(e){
				this.nickname=e.detail.value;
			},
			login_bupt: function(event){
				if(this.nickname.length>=8){
					uni.showToast({
						title:'昵称不能超过八位',
						icon:'none',
						duration:2000
					})
				}
				else{
					if(this.buptID.length===10){
						console.log(this.code)
						uni.request({
							url:'http://www.foolzy.top/login.php',
							data:{
								code:this.code,
								buptid:this.buptID,
								nickname:this.nickname
							},
							header:{
								'content-type':'application/x-www-form-urlencoded'
							},
							method:'POST',
							success: (res)=>{
								console.log(res.data);
								if(res.data.status === 1){
									uni.showToast({
									    title: '登录成功',
										icon:'success',
									    duration: 2000
									});
									uni.reLaunch({
										url:'../index/index'
									})
								}
								else if(res.data.status === 0){
									uni.showToast({
										title:'学号已存在',
										icon:'none',
										duration:2000
									})
								}
							}
						})
					}
					else{
						uni.showToast({
							title:'学号长度不符',
							icon:'none',
							duration:1000
						})
					}
				}
				
				
				
				// uni.navigateTo({
				//   url: '/pages/index/index',
				// })
			},
			login_none: function(){
				
				
			}
		},
		onLoad() {
			var that=this;
			wx.login({
				success:function(res){
					that.code=res.code
				}
			})
		}
	}
</script>

<style>
	.bk{
	    display: flex;
	    flex-direction: column;
	}
	.btn1{
	    width:80%;
		margin-top: 50rpx;
	}
</style>
