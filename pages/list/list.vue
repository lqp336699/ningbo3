<template>
	<view class="list">
		<view open-type="navigate"  v-for='(item,i) in listData'    class="listItem">
			
			<navigator :url="'/pages/listDetail/listDetail?id='+item.id"  open-type="navigate"  >
				<view class="img">
					<img :src="item.img" alt="">
				</view>
				<view class="title">
					<text>{{item.title}}</text>
				</view>
				<view class="pirce">
					<text>
						$  {{item.pirce}}
					</text>
					<view class="same">
						看相似
					</view>
				</view>
			</navigator>
			
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				listData:[]
			}
		},
		onShow(){
			uni.request({
				url:"http://localhost:5000/api/list",
				success: (res) => {
					if(res.success="1"){
						this.listData= res.data[0].listData;
						// console.log(JSON.stringify(this.listData))
					}
				}
			})	
		},
		methods:{
		
		}
	}
</script>

<style>
	.list{
		display:block;
		width:100%;
		background-color: #eee;
		overflow: hidden;
	}
	.listItem{
		display: block;
		width: 47vw;
		height:42vh;
		background-color: #fff;
		border-radius:3vw;
		overflow: hidden;
		margin:1vh 0 0 2vw;
		float:left;
	}
	.listItem .img{
		display: block;
		height:26vh;
		width: 100%;
	}
	.listItem .img img{
		width:100%;
		height:100%;
	}
	.listItem .title{
		display: block;
		font-size:3.7vw;
		margin:0 1vw;
		height: 6vh;
		width:47vw;
		text-overflow: ellipsis;
		overflow: hidden;
		margin-top: 2vh;
		display: -webkit-box; // 作为弹性伸缩盒子模型显示。
		-webkit-box-orient: vertical; // 设置伸缩盒子的子元素排列方式--从上到下垂直排列
		-webkit-line-clamp: 2; // 显示的行
	}
	.pirce{
		color:#fa2c19;
		margin-top: 1.3vh;
		font-weight:600;
		position:relative;
		text-indent:2vw;
	}
	.same{
		position:absolute;
		right: -2vw;
		top: 0;
		background-color: #f0f2f5;
		font-size:1vw;
		padding:0.5vw 2vw;
		border-radius:5vw;
		color:#aaa;
		font-weight:400
	}
</style>
