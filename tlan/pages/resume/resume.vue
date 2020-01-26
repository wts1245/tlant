<template>
	<view class="container">
		<view class="content" v-if="length>0">
			<view class="cu-item">
				<view class="text-grey">{{name}}</view>
				<view class="content">
					<view class="text-grey">期望工作地点：</view>
					<view class="text-gray text-content text-df">
						{{province}}{{cty}}{{area}}
					</view>
					<view class="bg-grey padding-sm radius margin-top-sm  text-sm">
						<view class="flex">
							<view>个人评价：</view>
							<view class="flex-sub"><textarea value="123121321" placeholder="" />{{evaluate}}</view>
						</view>
					</view>
					<view class="margin-top-sm flex justify-between">
						<view class="text-gray text-df"><view class="cu-tag bg-red light sm round">3000元</view></view>
						<view>
							<view class="cu-tag bg-red light sm round">{{post}}</view>
							<view class="cu-tag bg-green light sm round">{{state}}</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="watermark" v-else-if="length==0">
			<!-- <image src="../../static/image/sy.jpg" mode="" class=""></image> -->
			添加简历让你的boss早日找到你吧！！！
		</view>
		<view class="header">
			<tui-fab :left="left" :right="right" :bottom="bottom" :bgColor="bgColor" :btnList="btnList" @click="onClick"></tui-fab>
		</view>
	</view>
</template>
<script>
	import tuiButton from "@/components/extend/button/button"
	const thorui = require("@/components/utils/clipboard.thorui.js")
	import tuiFab from "@/components/tui-fab/tui-fab"
	export default {
		components: {
			tuiButton,
			tuiFab
		},
		data() {
			return {
				name:"",
				sex:"",
				city:"",
				state:"",
				evaluate:"",
				vitae:"",
				mailbox:"",
				phone:"",
				post:"",
				salary:"",
				province:"",
				cty:"",
				area:"",
				Certificates:"" ,
				length:"",
				left: 0,
				right: 80,
				bottom: 100,
				bgColor: "#5677fc",
				btnList: [],
				list: [{
					bgColor: "#16C2C2",
					//图标/图片地址
					imgUrl: "/static/image/zj.png",
					//图片高度 rpx
					imgHeight: 64,
					//图片宽度 rpx
					imgWidth: 64,
					//名称
					text: "增加",
					//字体大小
					fontSize: 34,
					//字体颜色
					color: "#fff"
				}, {
					bgColor: "#64B532",
					//图标/图片地址
					imgUrl: "/static/image/xg.png",
					//图片高度 rpx
					imgHeight: 64,
					//图片宽度 rpx
					imgWidth: 64,
					//名称
					text: "删除",
					//字体大小
					fontSize: 34,
					//字体颜色
					color: "#fff"
				}, {
					bgColor: "#FFA000",
					//图标/图片地址
					imgUrl: "/static/image/xc.png",
					//图片高度 rpx
					imgHeight: 64,
					//图片宽度 rpx
					imgWidth: 64,
					//名称
					text: "修改",
					//字体大小
					fontSize: 34,
					//字体颜色
					color: "#fff"
				}],

			}
		},
		onLoad(options) {
			this.btnList = [...this.list]
			try{
				var name = uni.getStorageSync("name");
				var sex = uni.getStorageSync("sex");
				var city = uni.getStorageSync("city");
				var state = uni.getStorageSync("state");
				console.log(state+'state')
				var evaluate = uni.getStorageSync("evaluate");
				var vitae = uni.getStorageSync("vitae");
				var mailbox = uni.getStorageSync("mailbox");
				var phone = uni.getStorageSync("phone");
				var post = uni.getStorageSync("post");
				console.log(post)
				var salary = uni.getStorageSync("salary");
				var Certificates = uni.getStorageSync("Certificates");
				var length = Certificates.length;
				this.length = length;
				console.log(length+"长度")
			}catch(e){
				//TODO handle the exception
			}
		this.name = name;
		this.sex = sex;
		if(city!=null){
			var province =city[0]
			this.province = province;
			var cty =city[1]
			this.cty = cty;
			var area=city[2]
			this.area = area;
		}else{
			console.log("空")
		}
		this.post = post;
		this.evaluate = evaluate;
		this.vitae = vitae;
		this.mailbox = mailbox;ss
		if(state==0){
			 var state1="在职";
			this.state = state1;
		}else if(state==1){
			var state2="离职";
			this.state=state2;
			console.log(state)
		}else{
			var state3="骑驴找马";
			this.state=state3
		}
		this.salary = salary;
		this.Certificates = Certificates;
		},
		onShow() {
			try{
				var name = uni.getStorageSync("name");
				this.name=name;
				var sex = uni.getStorageSync("sex");
				this.sex=sex;
				var city = uni.getStorageSync("city");
				if(city!=null){
					var province =city[0]
					this.province = province;
					console.log(province)
					var cty =city[1]
					this.cty = cty;
					var area=city[2]
					this.area = area;
				}else{
					console.log("空")
				}
				var state = uni.getStorageSync("state");
				console.log(state+'state1')
				var evaluate = uni.getStorageSync("evaluate");
				this.evaluate = evaluate;
				var vitae = uni.getStorageSync("vitae");
				this.vitae = vitae;
				var mailbox = uni.getStorageSync("mailbox");
				this.mailbox = mailbox;
				var phone = uni.getStorageSync("phone");
				this.phone = phone;
				var post = uni.getStorageSync("post");
				this.post = post;
				if(state==0){
					 var state1="在职";
					this.state = state1;
				}else if(state==1){
					var state2="离职";
					this.state=state2;
				}else{
					var state3="骑驴找马";
					this.state=state3
				}
				var salary = uni.getStorageSync("salary");
				this.salary = salary;
				var Certificates = uni.getStorageSync("Certificates");
				this.Certificates = Certificates;
				var length = Certificates.length;
				this.length = length;
				console.log(length)
			}catch(e){
				//TODO handle the exception
			}
		},
		methods: {
			change(type) {
				console.log(type + 'type')
				switch (type) {
					case 1:
						this.left = 80;
						this.right = 0;
						break;
					case 2:
						this.left = 0;
						this.right = 80;
						break;
					case 3:
						this.bgColor = "#FF0000";
						break;
					case 4:
						this.btnList = [];
						break;
					case 5:
						this.btnList = [...this.list];
						break;
					case 6:
						this.btnList = [...this.list2];
						break;
					default:
						break;
				}
				// this.tui.toast("切换成功，点击查看效果")
			},
			onClick(e) {
				let index = e.index
				console.log(e + 'onclick')
				switch (index) {
					case -1:
						// this.tui.toast("您点击了悬浮按钮")
						break;
					case 0:
						uni.navigateTo({
							url: "/pages/increase/increase"
						})
						break;
					case 1:
						// #ifdef MP || H5
						this.clipboard("https://thorui.cn/")
						// #endif
						//#ifdef APP-PLUS
						plus.share.sendWithSystem({
							content: "ThorUI组件库",
							href: 'https://thorui.cn/'
						}, function() {
							console.log('分享成功');
						}, function(e) {
							console.log('分享失败：' + JSON.stringify(e));
						});
						//#endif
						break;
					case 2:
						uni.previewImage({
							urls: ["https://thorui.cn/img/reward.jpg"]
						})
						break;
					default:
						break;
				}
			},
			clipboard: function(data) {
				thorui.getClipboardData(data, (res) => {
					if (res) {
						// this.tui.toast("分享链接已复制")
					} else {
						// this.tui.toast("分享链接复制失败")
					}
				})
			}
		}
	}
</script>

<style>
	.watermark{
		font-size: 40upx;
		font-family: KaiTi;
		font-style: inherit;
		padding: 0px;
		            width:500px;
		            height:200px;
		            text-align:center;
		            display: table-cell;
		            vertical-align:middle
	}
	.content{
		background-color:white ;
		margin-top: 20upx;
		height: 400upx;
		 margin: 0 auto;
		  width: 95%;
		  margin-top: 2%;
		  border: 1rpx solid white;
		  border-radius: 10rpx;
	}
	.container {
		padding: 20rpx 0 120rpx 0;
		box-sizing: border-box;
	}

	.header {
		padding: 80rpx 90rpx 60rpx 90rpx;
		box-sizing: border-box;
	}

	.title {
		font-size: 34rpx;
		color: #333;
		font-weight: 500;
	}

	.sub-title {
		font-size: 24rpx;
		color: #7a7a7a;
		padding-top: 18rpx;
	}

	.tui-btn-box {
		padding: 10rpx 40rpx;
		box-sizing: border-box;
	}

	.tui-btn-btm {
		margin-bottom: 36rpx;
	}
</style>
