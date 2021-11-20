<template>
	<view>
		<view class="name" v-show=" !userInfo.username ? true : false ">
			<login></login>
		</view>
		<view class="top" v-show=" userInfo.username ? true : false ">
			<view class="topt">
				<view>
					<img src="@/static/logo.png" alt="">
				</view>
				<view class="text">
					<view class="name" >{{userInfo.username}}</view>
					<view>
						<span class="num">0 粉丝</span>
						<span class="num">0 关注</span>
					</view>
				</view>
				<view class="setup">
					<span class="iconfont">&#xe601;</span>
				</view>
				
			</view>
			<view class="name">
				<button type="primary" @click="back">退出登录</button>
			</view>
		</view>
	</view>
</template>

<script>
	import login from './../login/login'
	export default{
		components:{login},
		data(){
			return{
				userInfo:{}
			}
		},
		onShow(){
			this.userInfo = { ...getApp().globalData.userInfo }//取值全局变量
			
		},
		methods:{
			back(){
				uni.removeStorage({
					key: 'userInfo',
					    success: function (res) {
					        console.log('success');
							getApp().globalData.userInfo=false;
							uni.reLaunch({
								url: '/'
							})
					    }
				})
			}
		}
		}
</script>

<style>
	.topt{
		display: flex;
		justify-content:space-between;
		padding:3vh 2vw;
		align-items: center;
	}
	.topt img{
		border-radius:50%;
		width: 12vw;
		height: 12vw;
	}
	.text{
		margin-right: 40vw;;
	}
	.text view{
		margin-bottom: 2vh;
	}
	.num{
		font-size:2vw;
		color:#777;
		margin-right:2vw;
	}
	.name{
		font-weight:600;
	}
	.setup{
		margin-bottom:2vh;
		margin-right: 6vw;
	}
</style>
