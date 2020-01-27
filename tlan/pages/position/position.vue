<template>
	<view>
		<view class="padding ">
			<view class="padding-xl radius shadow bg-white" @click="position" >
				<view class="container">
					网络工程师	
				</view>
				<view class="text-center">
					北京中科曙光有限公司
				</view>
				<view class="text-left">
					公司简介：
				</view>
				<view class="text-left nb">
					
					第9次夺得中国高性能计算机TOP100份额排行榜第一名
					获批牵头组建国家先进计算产业创新中心
				</view>
				<view class="text-right">
				<view class="cu-tag round bg-orange light">3年以上</view>
				<view class="cu-tag round bg-olive light">3000-5000</view>
				<view class="cu-tag round bg-blue light">本科以上</view>
				</view>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
			
			}
		},
		onLoad() {
			// 获取职位信息
			uni.request({
				url:'',
				data:{
					
				},
				method:'POST'
			})
		},
		methods: {
		position(e){
			uni.navigateTo({
				url:'../details/details'
			})
		}
		}
	}
</script>

<style>
	.padding-xl {
		margin-left: 10upx;
	}

	.inside {
		height: 280upx;
		background-color: #9C26B0;
	}

	.nb {
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap;
	}
</style>
