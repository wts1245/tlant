<template>
	<view class="container">
		<view class="header">
			<view class="cu-card case" :class="isCard?'no-card':''">
				<view class="cu-item shadow">
					<view class="image">
						<image src="https://ossweb-img.qq.com/images/lol/web201310/skin/big10006.jpg"
						 mode="widthFix"></image>
						<view class="cu-tag bg-blue">网络工程师</view>
						<view class="cu-bar bg-shadeBottom"> <text class="text-cut">我已天理为凭，踏入这片荒芜，不再受凡人的枷锁遏制。我已天理为凭，踏入这片荒芜，不再受凡人的枷锁遏制。</text></view>
					</view>
					<view class="cu-list menu-avatar">
						<view class="cu-item">
						
							<view class="content flex-sub">
								<view class="text-grey">正义天使 凯尔</view>
								<view class="text-gray text-sm flex justify-between">
									十天前
									<view class="text-gray text-sm">
										<text class="cuIcon-attentionfill margin-lr-xs"></text> 10
										<text class="cuIcon-appreciatefill margin-lr-xs"></text> 20
										<text class="cuIcon-messagefill margin-lr-xs"></text> 30
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
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
			console.log(options)
			this.btnList = [...this.list]
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
				this.tui.toast("切换成功，点击查看效果")
			},
			onClick(e) {
				let index = e.index
				console.log(e + 'onclick')
				switch (index) {
					case -1:
						this.tui.toast("您点击了悬浮按钮")
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
						this.tui.toast("分享链接已复制")
					} else {
						this.tui.toast("分享链接复制失败")
					}
				})
			}
		}
	}
</script>

<style>
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
