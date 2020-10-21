<script>
	export default {
		globalData:{
			isLogin:0
		},
		onLaunch: function() {
			console.log('App Launch')
			const that=this;
			wx.login({
				success:function(res){
					console.log(res)
					var code=res.code
					console.log(code)
					wx.request({
						url:'http://www.foolzy.top/check.php',
						method:'POST',
						header:{
							'content-type':'application/x-www-form-urlencoded'
						},
						data:{
							code:code,
						},
						success:function(res){
							const app=getApp()
							app.globalData.isLogin=parseInt(res.data.status)
							console.log(app.globalData.isLogin)
						}
					})
				}
			})
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>
	
<style>
	/*每个页面公共css */
	@import "colorui/main.css";
	@import "colorui/icon.css";
</style>
