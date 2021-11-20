<template>
	
	<view class='content'>
		
			<view class="login_register">
				<view class="btns">
					<view class="login" :class="active=='登录'? 'active':''"  @click="isactive()" >登录</view>
					<view class="register" :class="active=='注册'? 'active':'' " @click="isntactive()">注册</view>
				</view>
			</view>
			
			<view class="inps">
					<input type="text" v-model="username"   placeholder-style="color:white" placeholder="手机号"   />
					<input type="text" v-model="password"  placeholder-style="color:white" placeholder="密码"   />
			</view>
			<uni-popup ref="popup" type="message">
			    <uni-popup-message type="success" message="注册成功自动登录" :duration="2000"></uni-popup-message>
			</uni-popup>
			<uni-popup ref="popup2" type="message">
			    <uni-popup-message type="success" message="正在登录" :duration="2000"></uni-popup-message>
			</uni-popup>
			<button class="reb" @click="nav()" >{{active}}</button>		
	</view>
	<!-- 本地背景图片的引用路径推荐使用以 ~@ 开头的绝对路径。
	 .test2 {
	     background-image: url('~@/static/logo.png');
	 } -->
</template>

<script>
	export default{
		name:'login',
		data() {
			return {
				active:"登录",
				username:'',
				password:"",
				islogin:false
			}
		},
		methods:{
			
			isactive(){
				this.active="登录";
			},
			isntactive(){
				this.active="注册";		
			},	
			nav (){
				let userInfo = {"username":this.username,"password":this.password}
				let _this = this;
				if(userInfo.username.length!==11 ){
					uni.showModal({
						content: '手机号错误'
					})
					return false;
				}
				if(userInfo.password.length=='' ){
					uni.showModal({
						content: '请填写密码'
					})
					return false;
				}
				if(this.active=="注册"){
					uni.request({
						url:"http://localhost:5000/api/regiest",
						method:"POST",
						data:userInfo,
						success:(res)=>{
							// console.log(res.data.success)
							if(res.data.success==1){
								uni.setStorage({
								    key: 'userInfo',
								    data:userInfo,
								    success: function () {
										_this.$refs.popup.open('top')
										// getApp().globalData.userInfo=userInfo;
										_this.islogin=true;
										_this.$emit("isLogin",_this.islogin)
										setTimeout(()=>{
											uni.reLaunch({
												url:"../my/my"
											});
										},2000)		
								    }
								});
							}else{
								uni.showModal({
									content: '手机号已注册'
								})
							}
						}
					})
				}else{
					uni.request({
						url:"http://localhost:5000/api/login",
						method:"POST",
						data:userInfo,
						success:((res)=>{
							let success = res.data.success;
							if(success=="1"){
								// console.log("登录成功")
								uni.setStorage({
								    key: 'userInfo',
								    data:userInfo,
								    success: function () {
										_this.$refs.popup2.open('top');
										// getApp().globalData.userInfo=userInfo;
										_this.islogin=true;
										_this.$emit("isLogin",_this.islogin)
										setTimeout(()=>{
											uni.reLaunch({
												url:"../my/my"
											});
										},2000)		
								    }
								});
							}else if(success=="密码错误"){
								console.log("密码错误")
								uni.showModal({
									content: '密码错误'
								})
							}else if(success == "手机号未注册"){
								uni.showModal({
									content: '手机号未注册'
								})
							}
						})
					})
				}
			}
		}
	}
</script>

<style>
	view{
		display: block;
	}
	button{
		margin: 0;
		padding:0;
	}
	.inps input{
		background-color: rgb(105,105,142);
		height:7.5vh;
		border-radius:2vw;
		text-indent:5vw;
		font-size:3.6vw;
		color:white;
		margin-top: 3vh;
	}
	.content{
		display:block;
		font-size:2vw;
		display: flex;
		justify-content: center;
		flex-direction:column;
		padding:11vw;
	}
	
	.login_register{
		height:6vh;
		width: 37.3vw;
		display: flex;
		margin-left: -5vw;
		margin-bottom: 3vh;
	}
	.btns{
		color:#fff;
		display: flex;
		width:33vw;
		border-radius:6vw;
		overflow: hidden;
		line-height:6vh;
		text-align:center;
	}
	
	.register{
		height:6vh;
		width: 16.5vw;
		background-color:rgb(51,51,102);
	}
	.login{
		height:6vh;
		width: 16.5vw;
		background-color:rgb(51,51,102);
	}
	
	
	
	.inps input::-webkit-input-placeholder {
		color: red;
	}
	::-moz-placeholder {/* Firefox 18- */
	  color: red;
	}
	::-moz-placeholder{/* Firefox 19+ */
	 color: red;
	}
	::-ms-input-placeholder {
	  color: red;
	}
	
	.inps{
		margin-bottom:4vh;
		display: block;
	}
	
	.inp{
		margin-top: 4vh;
	}
	
	.reb{
		background-color:rgb(51,204,102) ;
		border-radius: 4vw;
		color:white;
		display: block;
		height:7.5vh;
		width: 78vw;
		line-height: 7.5vh;
	}
	.active{
		background-color:rgb(255,102,102);
	}
		
</style>
