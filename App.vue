<script>
	export default {
		data(){
			return{
				globalData:{
					userInfo,
				}
			}
		},
		created(){
			// let _this = this;
			// uni.getStorage({
			//     key: 'userInfo',
			//     success: function (res) {
			//         console.log(res.data);
			// 		if(res.data){
			// 			let userInfo = { ...res.data };
			// 			getApp().globalData.userInfo=userInfo;//定义全局变量
			// 		}else{
			// 			getApp().globalData.userInfo=false;
			// 		}	
			//     }
			// });
		},
		onShow: function() {
			let _this = this;
				uni.getStorage({
				    key: 'userInfo',
				    success: function (res) {
						let userInfo = { ...res.data };
						getApp().globalData.userInfo=userInfo;//定义全局变量
				    },
					fail:()=>{
						getApp().globalData.userInfo=false;
					}
				});
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	view{
		display: block;
	}
</style>
