<template>
	<view class="">
		<view class="srcoll_view" bindtap="textclick">为了您能及时了解求职信息，请务必填写真实信息</view>

		<view class="">
			基本信息
		</view>
		<view class="">
			<form @submit="formSubmit">
				<view class="cu-form-group margin-top">
					<view class="title">姓名</view>
					<input placeholder="输入姓名" name="name"></input>
				</view>
				<view class="cu-form-group">
					<view class="title">年龄</view>
					<input placeholder="输入年龄" name="age"></input>
				</view>
				<view class="cu-form-group">
					<view class="title">验证码</view>
					<input placeholder="输入框带个按钮" name="input"></input>
					<button class='cu-btn bg-green shadow' @tab="Verification">验证码</button>
				</view>
				<view class="cu-form-group">
					<view class="title">手机号码</view>
					<input placeholder="输入框带标签" name="input"></input>
					<view class="cu-capsule radius">
						<view class='cu-tag bg-blue '>
							+86
						</view>
						<view class="cu-tag line-blue">
							中国大陆
						</view>
					</view>
					</view>
				<view class="cu-form-group">
					<view class="title">居住地</view>
					<input placeholder="居住地" name="country"></input>
					<text class='cuIcon-locationfill text-orange'></text>
				</view>
				<radio-group name="sex">
					<label>
						<radio :value="0" /><text>男</text>
						<radio :value="1" /><text>女</text>
					</label>
				</radio-group>

				<view class="padding flex flex-direction">
					<button class="cu-btn block bg-blue margin-tb-sm lg" form-type="submit">提交</button>
				</view>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name: '',
				age: '',
				phoneNum: '',
				country: '',
				sex: ''
			}
		},
		onLoad(options) {
			console.log(options)
		},
		methods: {
			formSubmit(e) {
				var name = e.detail.value.name;
				var age = e.detail.value.age;
				var phoneNum = e.detail.value.phoneNum;
				var country = e.detail.value.country;
				var sex = e.detail.value.sex;
				console.log(name)
			},
			Verification(){
				
			}
		}
	}
</script>

<style>
	.srcoll_view {
		position: absolute;
		top: 0rpx;
		height: 100rpx;
		font-size: 30rpx;
		white-space: nowrap;
		line-height: 100rpx;
		color: #E54D42;
		animation: myfirst 20s linear infinite;
	}

	@keyframes myfirst {
		0% {
			margin-left: 750rpx;
		}

		100% {
			margin-left: -1500rpx;
		}
	}

	.scroll_view_border {
		position: relative;
		width: 100%;
		background: #E54D42;
		height: 100rpx;
		overflow: hidden;
	}
</style>
