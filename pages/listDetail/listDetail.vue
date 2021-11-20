<template>
	<view class="box">
		<view class="swiperBox">
			<swiper class="swiper" 
					:indicator-dots="indicatorDots" 
					:easing-function="easingFunction" 
					:autoplay="autoplay" 
					:interval="interval" 
					:duration="duration"  
					@change="getIndex()">
					
			     <swiper-item v-for="(item,index) in swiper" calss="si" :keys="index">
			         <view class="swiper-item uni-bg-red">
						 <img class="img" :src="item.img" alt="">
					 </view>
			     </swiper-item>
			</swiper>
			<view class="page">
				 1/{{this.swiper.length}}
			</view>
		</view>
		<view class="footNav">
			<tabBar></tabBar>
		</view>
		<view class="title">
			<view class="pirce">
				$ 129. <span>00</span> 
			</view>
			<view class="text">
				都市丽人内衣女2021春季新品无钢圈乳胶棉超薄杯大胸显小胸罩花瓣蕾丝随意裁上托防垂文胸2B13A3 
				紫兰 34/75B
			</view>
		</view>
		<view class="safe">
			<span class="img"></span>
			<span class="text"> 免费上门取退 极速审核 24H发货</span>
			<span class="iconfont" @click="open"> &#xe600;</span>
		</view>
		<uni-popup ref="popup" type="bottom">
			<view class="pop">
				<view class="closet iconfont" @click="close"> &#xe61b;</view>
				<view class="popTitle">
					放心购
				</view>
				<view class="popItem">
					<view class="popItemTitle">免费上门退取</view>
					<view class="popItemb">京东快递免费上门取退，取退后闪电退款</view>
				</view>
				<view class="popItem">
					<view class="popItemTitle">极速审核</view>
					<view class="popItemb">极速审核指商家为用户提供的针对售后退换货流程的专项服务，开通后售后服务单会在24H内审核完毕；</view>
				</view>
				<view class="popItem">
					<view class="popItemTitle">24H发货</view>
					<view class="popItemb">24点前下单，24小时内发货</view>
				</view>
				<button class="btn" @click="close" type="warn">确认</button>
			</view>	
		</uni-popup>
		<view v-for="item in 5">
			<view class="safeb safe" @click="open">
				<span class="text1"> 优惠</span>
				<view class="yhm">
					<view class="textBox">
						<span class="text2"> 满300-30</span>
					</view>
					<view class="textBox">
						<span class="text2"> 满减</span>
						<span class="text3">满200元减70元，满300元减80元</span>
					</view>
					<view class="textBox">
						<span class="text2">多买优惠</span>
						<span class="text3">满200元减70元，满300元减80元</span>
					</view>
					<view class="textBox">
						<span class="text2">限购</span>
						<span class="text3">满200元减70元，满300元减80元</span>
					</view>
				</view>
				<span class="iconfont" > &#xe600;</span>
			</view>
		</view>
	</view>	
	</view>
</template>

<script>
	import tabBar from '@/components/tabBar/tabBar'
	export default{
		components:{tabBar},
		data(){
			return{
				id:0,
				background: ['color1', 'color2', 'color3'],
				indicatorDots: false,
				autoplay: false,
				interval: 2000,
				duration: 500,
				easingFunction:"linear",
				index:1,
				swiper:[
					
				]
			}
		},
		onLoad(options){
			this.id=options.id,
			uni.request({
				url:'http://localhost:5000/api/list/detail?_id='+this.id,
				success:(res)=>{
					console.log(res.data[0].data)
					this.swiper = res.data[0].data
				}
			})
			
		},
		methods:{
			getIndex(current){
				// console.log(current)
			},
			open(){
			        // 通过组件定义的ref调用uni-popup方法 ,如果传入参数 ，type 属性将失效 ，仅支持 ['top','left','bottom','right','center']
			        this.$refs.popup.open()
			      },
			close(){
				this.$refs.popup.close()
			}	  
		},
		onShow(){
			
		}
	}
</script>

<style>
	.box{
		position: relative;
		background-color: #f2f2f2; 	
	}
	.swiperBox{
		position: relative;
	}
	.img{
		width: 100%;
		height:100%;
	}
	
	.swiper{
		height: 57vh;
	}
	.swiperBox .page{
		display: block;
		width:14vw;
		height: 3vh;
		position: absolute;
		text-align: center;
		line-height:3vh;
		bottom:2vh;
		right:-2vw;
		border-radius:4vw;
		color:#ececec;
		font-size:4vw;
		background-color: rgba(0,0,0,0.3);
	}
	.footNav{
		position:fixed;
		bottom:0;
		right: 0;
		left:0;
	}
	.title{
		font-weight:600;
		padding:1vh;
		background-color: #fff;
	}
	.title .pirce{
		color:red;
		font-size:6vw;
		margin-bottom: 2vh;
	}
	.title .pirce span{
		font-size:5vw;
		font-weight:400;
	}
	.safe{
		height:4vh;
		background-color: #fbf0fd;
		padding:1vh 6vw;
		display: flex;
		justify-content:space-around;
		align-items:center;
	}
	.safe .img{
		background: url("@/static/icon.png")  0 center no-repeat;
		background-size:18vw 2vh;
		display: block;
		width:20vw;
	}
	.safe .text{
		font-size:3vw;
		margin-right: 14vw;;
		
	}
	
	.pop{
		height: 60vh;
		background-color: #fff;
		border-radius:4vw;
		position:relative;
		bottom:-2vh;
	}
	.popTitle{
		text-align:center;
		font-size:4vw;
		font-weight:600;
		padding:2vh 0;
	}
	.popItem{
		font-size:4vw;
		border-bottom:1px solid #eee;
		margin:0 4vw;
		padding:2vh 0;
	}
	.popItemTitle{
		color:red;
		display: block;
		margin-bottom: 1vh;
	}
	.popItemb{
		font-size:2vw;
		color:#555;
	}
	.pop .btn{
		width:90vw;
		border-radius:5vw;
		position:absolute;
		bottom:3vh;
		right: 0;
		left: 0;
	}
	.closet{
		position:absolute;
		top: 6vw;
		right: 6vw;
		font-size:3vw;
		background-color: #eee;
		border-radius:50%;
		padding:0.5vw;
	}
	.safeb{
		background-color: #fff;
		display:flex;
		align-item:center;
		justify-content:space-between;
		height: 20vh;
		align-items: flex-start;
		margin-top: 2vh;
		border-radius:3vw;
		
	}
	.safeb .text2{
		color:red;
		font-size:3vw;
		margin-right: 50vw;
	}
	.safeb .text1{
		color:#000;
		width: 20vw;
		font-weight:600;
	}
	.yhm{
		display: flex;
		justify-content:space-between;
		flex-direction:column;
	}
	.textBox{
		margin-top:1vh;
	}
	
	.textBox .text2{
		display: inline;
		margin: 0 2vw 0 0;
	}
	.textBox .text3{
		font-size:3vw;
	}
	
</style>
