<template>
	<view >
		<view >
			<!-- <cmd-cell-item title="姓名" addon="{{name}}"/>
			<cmd-cell-item title="性别" addon="{{sex}}"/>
			<cmd-cell-item title="年龄" addon="{{age}}"/>
			<cmd-cell-item title="证件号" addon="{{num}}"/>
			<cmd-cell-item title="居住地" addon="{{country}}"/> -->
			<navigator url="../modify/modify" hover-class="navigator-hover">
				<!-- <cmd-cell-item  addon="修改" arrow/> -->
				<view class="" @click="test">
					修改
				</view>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				name:"",
				sex:"",
				age:"",
				num:"",
				country:""
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	navigator:hover{
		background-color: #007AFF;
	}
</style>
