<template>
	<view>
		<form @submit="formSubmit">
			<view class="cu-form-group margin-top">
				<view class="title">姓名:</view>
				<input placeholder="姓名" name="name"></input>
			</view>

			<view class="cu-form-group margin-top">
				<view class="title">邮箱:</view>
				<input placeholder="邮箱" name="mailbox"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">性别:</view>
				<input placeholder="性别" name="sex"></input>
			</view>
			<view class="cu-form-group">
				<view class="title">电话:</view>
				<input placeholder="电话" name="phone"></input>
			</view>

			<view class="cu-form-group">
				<view class="title">证件号:</view>
				<input placeholder="身份证" name="Certificates"></input>
			</view>

			<view class="cu-form-group">
				<view class="title">求职岗位:</view>
				<input placeholder="求职岗位" name="post"></input>
			</view>

			<view class="cu-form-group">
				<view class="title">期望月薪:</view>
				<input placeholder="期望月薪" name="salary"></input>
			</view>

			<view class="cu-form-group">
				<view class="title">工作状态:</view>
				<radio-group name="state">
					<label>
						<radio :value="0" /><text>在职</text>
						<radio :value="1" /><text>离职</text>
						<radio :value="2" />骑驴找马<text></text>
					</label>
				</radio-group>
			</view>
			<view class="cu-form-group">
				<view class="title">期望工作地点:</view>
				<view>
					<view @tap="togglePopup('bottom','popup')" style="padding: 40upx;display: flex;align-items: center;">
						<view v-for="(item, index) in selectList" :key="index">
							{{item.txt}}<span v-show="index == 0 || index == 1">—</span>
						</view>
					</view>
					<uni-popup ref="popup" :type="type" @change="change">
						<view class="select-border">
							<view class="header">
								<view class="title">
									选择地区
								</view>
								<view class="cancel-icon" @tap="cancel('popup')">
									X
								</view>
							</view>
							<view class="select-box">
								<view class="select-item">
									<view class="select-list" @tap="tabEvent(index)" :class="indexTab == index ? 'selected' : ''" v-for="(item, index) in selectList"
									 :key="index">
										{{item.txt}}
									</view>
								</view>
								<view class="select-item-box">
									<!-- 省 -->
									<view class="province-box" v-show="proviceShow">
										<view class="select-list-cont" @tap="provinceEvent(item,index)" v-for="(item,index) in provinceData" :key="item.code">
											{{item.name}}<span class="check" v-show="index == checkOne">√</span>
										</view>
									</view>
									<!-- 市 -->
									<view class="city-box" v-show="cityShow">
										<view class="select-list-cont" @tap="cityEvent(item,index)" v-for="(item,index) in cityData" :key="item.code">
											{{item.name}}<span class="check" v-show="index==checkTwo">√</span>
										</view>
									</view>
									<!-- 区 -->
									<view class="area-box" v-show="areaShow">
										<view class="select-list-cont" @tap="areaEvent(item,index)" v-for="(item,index) in areaData" :key="item.code">
											{{item.name}}<span class="check" v-show="index==checkThree">√</span>
										</view>
									</view>
								</view>
							</view>
						</view>
					</uni-popup>
				</view>
			</view>
			<view class="cu-form-group align-start">
				<view class="title">工作履历:</view>
				<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaAInput" placeholder="工作履历"></textarea>
			</view>
			<view class="cu-form-group align-start">
				<view class="title">自我评价:</view>
				<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaBInput" placeholder="自我评价"></textarea>
			</view>

			<view class="padding flex flex-direction">
				<button class="cu-btn block bg-blue margin-tb-sm lg" @tap='test' form-type="submit">提交</button>
			</view>
		</form>
	</view>
</template>

<script>
	import cityDatas from '@/components/city-data/city.area.js'
	import uniPopup from '@/components/city-data/uni-popup.vue'
	export default {
		components: {
			uniPopup
		},
		data() {
			return {
				provinceData: cityDatas,
				cityData: [],
				areaData: [],
				selectList: [{
					txt: '请选择'
				}, {
					txt: '请选择'
				}, {
					txt: '请选择'
				}],
				tabOne: '请选择',
				indexTab: 0,
				proviceShow: true,
				areaShow: false,
				cityShow: false,
				show: false,
				type: '',
				checkOne: null,
				checkTwo: null,
				checkThree: null,
				city: [],
				evaluate: '',
				vitae: '',
				mailbox: '',
				sex: '',
				phone: '',
				post: '',
				salary: '',
				state: '',
				name: '',
				Certificates: ''
			}
		},
		methods: {
			formSubmit(e) {
				console.log(e)
				this.Certificates = e.detail.value.Certificates;
				this.name = e.detail.value.name;
				this.mailbox = e.detail.value.mailbox;
				this.sex = e.detail.value.sex;
				this.phone = e.detail.value.phone;
				this.post = e.detail.value.post;
				this.salary = e.detail.value.salary;
				this.state = e.detail.value.state;
				
				if (this.name == null && this.Certificates == null && this.sex == null && this.city == null && this.evaluate == nul &&
					this.vitae == null && this.phone == null && this.post && this.salary == null && this.state == null && this.mailbox
				) {
					uni.showToast({
						title: '请填写完整信息！！！',
						icon: 'fail',
						duration: 1000,
						mask:true
					})
				} else {
					uni.setStorageSync("name",this.name)
					setTimeout(() => {
						uni.redirectTo({
							url: "../modify/modify?name=" + this.name,
						});
					}, 600);
				}
			},
			test(){
				var tt = this.name
				console.log(tt)
			},
			textareaAInput(e) {
				var vitae = e.detail.value;
				this.vitae = vitae
			},
			textareaBInput(e) {
				var evaluate = e.detail.value;
				this.evaluate = evaluate

			},
			togglePopup(type, open) {
				this.type = type
				if (open === 'tip') {
					this.show = true
				} else {
					this.$refs[open].open()
				}
			},
			cancel(type) {
				if (type === 'tip') {
					this.show = false
					return
				}
				this.$refs[type].close()
			},
			change(e) {
				if (e.show == true) {
					uni.hideTabBar()
				} else {
					uni.showTabBar()
				}
			},
			tabEvent(index) {
				this.indexTab = index
				if (this.indexTab == 0) {
					this.proviceShow = true
					this.cityShow = false
					this.areaShow = false
					// this.checkOne = null
					this.checkTwo = null
					this.checkThree = null
					// this.cityData = []
					this.areaData = []
					// this.selectList[0].txt = "请选择"
					this.selectList[1].txt = "请选择"
					this.selectList[2].txt = "请选择"
				} else if (this.indexTab == 1) {
					this.proviceShow = false
					this.cityShow = true
					this.areaShow = false
					// this.checkTwo = null
					this.checkThree = null
					// this.areaData = []
					// this.selectList[1].txt = "请选择"
					this.selectList[2].txt = "请选择"
				} else if (this.indexTab == 2) {
					this.proviceShow = false
					this.cityShow = false
					this.areaShow = true
				}
			},
			//省级选择
			provinceEvent(data, index) {
				console.log(data)
				var city = data.name;
				this.city[0] = city;
				this.checkOne = index
				this.selectList[0].txt = data.name
				this.indexTab = 1
				this.proviceShow = false
				this.cityShow = true
				this.areaShow = false
				this.cityData = data.cityList
			},
			// 市级选择
			cityEvent(data, index) {
				var city = data.name;
				this.city[1] = city;
				this.checkTwo = index
				this.selectList[1].txt = data.name
				this.indexTab = 2
				this.proviceShow = false
				this.cityShow = false
				this.areaShow = true
				this.areaData = data.areaList
			},
			// 地区级
			areaEvent(data, index) {
				var area = data.name;
				this.city[2] = area;
				console.log(this.city[2])
				this.checkThree = index
				this.selectList[2].txt = data.name
			}
		}
	}
</script>

<style>
	.header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 35upx;
	}

	.title {
		font-size: 34upx;
		font-family: PingFang SC;
		font-weight: bold;
		color: rgba(51, 51, 51, 1);
	}

	.cancel-icon {
		font-size: 34upx;
		color: rgba(153, 153, 153, 1);
	}

	.check {
		padding-left: 17upx;
		color: #FF7E28;
	}

	.select-box {
		height: 1024upx;
	}

	.select-item {
		display: flex;
		align-items: center;
		padding-left: 50upx;
		margin-bottom: 20upx;
		border-bottom: 1px solid #F6F6F6;
	}

	.select-list {
		width: 120upx;
		height: 40upx;
		text-align: center;
		overflow: hidden;
		/*超出部分隐藏*/
		text-overflow: ellipsis;
		/* 超出部分显示省略号 */
		white-space: nowrap;
		/*规定段落中的文本不进行换行 */
		font-size: 30upx;
		font-family: PingFang SC;
		font-weight: bold;
		color: rgba(51, 51, 51, 1);
		margin-right: 30upx;
		border-bottom: 1px solid #FFFFFF;
	}

	.select-list-cont {
		padding-left: 67upx;
		font-size: 30upx;
		font-family: PingFang SC;
		font-weight: 500;
		color: rgba(51, 51, 51, 1);
		line-height: 40px;
	}

	.selected {
		border-bottom: 1px solid #F0AD4E;
		color: rgba(255, 133, 0, 1);
	}
</style>
