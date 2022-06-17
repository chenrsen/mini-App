<template>
	<view class="wrapper">
		<uni-nav-bar fixed left-icon="left" @clickLeft="navigateBack" title="加入我们"></uni-nav-bar>
		<view class="container">
			<uni-forms ref="form" :modelValue="formData" :rules="rules" label-position="top">
				<uni-forms-item label="会员类型" name="memberType">
					<view class="text" v-model="formData.memberType">个人会员</view>
				</uni-forms-item>
				<uni-forms-item label="等级" name="memberLevel">
					<view class="text" v-model="formData.memberLevel">普通会员</view>
				</uni-forms-item>
				<uni-forms-item label="用户名" name="userName">
					<view class="text" v-model="formData.userName">566556</view>
					<view class="right_text">同步绿色国网</view>
				</uni-forms-item>
				<uni-forms-item label="姓名" name="memberName" required>
					<uni-easyinput type="text" v-model="formData.memberName" placeholder="请输入姓名" />
				</uni-forms-item>
				<uni-forms-item label="出生年月" name="birthday" required>
					<uni-datetime-picker type="date" v-model="formData.birthday" placeholder='请选择出生年月' />
				</uni-forms-item>
				<uni-forms-item label="性别" name="genderCode" required>
					<uni-data-checkbox v-model="formData.genderCode" :localdata="sexs"  @change="genderChange" />
				</uni-forms-item>
				<uni-forms-item label="政治面貌" name="politics" required>
					<picker v-model="formData.politics" :range="polData" :value="polIndex" @change="politicsChange">
						<view class="uni-input">{{polData[polIndex]}}</view>
					</picker>
				</uni-forms-item>
				<uni-forms-item label="联系地址" name="addressCode" required>
					<uni-data-picker :localdata="dataTree" v-model="formData.addressCode" placeholder="请选择联系地址" popup-title="请选择所在地区" @change="addressChange">
					</uni-data-picker>
				</uni-forms-item>
				<uni-forms-item label="手机号" name="phoneNumber">
					<view class="text" v-model="formData.phoneNumber">13069548759</view>
					<view class="right_text">同步绿色国网</view>
				</uni-forms-item>
				<!-- <view>
					<view class="label">登录手机号</view>
					<view class="text" v-model="formData.phoneNumber">13069548759</view>
					<view class="right_text">同步绿色国网</view>
				</view> -->
				<uni-forms-item label="邮箱" name="email" required>
					<uni-easyinput type="text" v-model="formData.email" placeholder="请输入邮箱" />
				</uni-forms-item>
				<uni-forms-item label="分支机构" name="branch">
					<view class="text" v-model="formData.branch">综合能源服务专业委员会</view>
				</uni-forms-item>
				<uni-forms-item label="工作单位" name="unit" required>
					<uni-easyinput type="text" v-model="formData.unit" placeholder="请输入工作单位" />
				</uni-forms-item>
				<uni-forms-item name="protocolId">
					<uni-data-checkbox v-model="formData.protocolId" :localdata="proData"  @change="protocolChange" required />
				</uni-forms-item>
			</uni-forms>
		</view>
		<button type="primary" @click="submit">申请加入</button>
	</view>
</template>

<script>
export default {
	data() {
		return {
			formData: {
				memberType: '个人会员',
				memberLevel: '普通会员',
				userName: '566556',
				memberName: '',
				birthday: '',
				genderCode: '',
				genderName: '',
				politics: '中共党员',
				addressCode: '',
				addressName: '',
				phoneNumber: '13069548759',
				branch: '综合能源服务专业委员会',
				unit: '',
				protocolId: '',
				protocolName: '',
			},
			sexs: [
				{  value: 0, text: '男', },
				{  value: 1, text: '女', },
			],
			polData: [ '中共党员', '中共预备党员', '共青团员', '无党派人士', '群众' ],
			polIndex: 0,
			proData: [{ value: 0, text: '已认真阅读并同意综合能源服务专委会会员协议',}],
			dataTree: [
				{
					value: "4401",
					text: "广州市",
					children: [
						{  value: "440103", text: "荔湾区", },
						{  value: "440104", text: "越秀区", },
						{  value: "440105", text: "海珠区", },
						{  value: "440106", text: "天河区", },
						{  value: "440111", text: "白云区", },
						{  value: "440112", text: "黄埔区", },
						{  value: "440113", text: "番禺区", },
						{  value: "440114", text: "花都区", },
						{  value: "440115", text: "南沙区", },
						{  value: "440116", text: "萝岗区", },
						{  value: "440183", text: "增城市", },
						{  value: "440184", text: "从化市", },
					]
				},
				{
					value: "4403",
					text: "深圳市",
					children: [
						{  value: "440303", text: "罗湖区", },
						{  value: "440304", text: "福田区", },
						{  value: "440305", text: "南山区", },
						{  value: "440306", text: "宝安区", },
						{  value: "440307", text: "龙岗区", },
						{  value: "440308", text: "盐田区", },
						{  value: "440309", text: "龙华区", },
						{  value: "440310", text: "坪山区", },
						{  value: "440311", text: "光明区", },
					]
				},
				{
					value: "4406",
					text: "佛山市",
					children: [
						{  value: "440604", text: "禅城区", },
						{  value: "440605", text: "南海区", },
						{  value: "440606", text: "顺德区", },
						{  value: "440607", text: "三水区", },
						{  value: "440608", text: "高明区", },
					]
				},
			],
			rules: {
				memberName: {
					rules: [
						{ required: true, errorMessage: '请输入姓名', },
						{ minLength: 3, maxLength: 5, errorMessage: '姓名长度在 {minLength} 到 {maxLength} 个字符', }
					]
				},
				birthday: {
					rules: [
						{ required: true, errorMessage: '请选择出生年月', },
					]
				},
				genderCode: {
					rules: [
						{ required: true, errorMessage: '请选择性别', },
					]
				},
				politics: {
					rules: [
						{ required: true, errorMessage: '请选择政治面貌', },
					]
				},
				addressCode: {
					rules: [
						{ required: true, errorMessage: '请选择联系地址', },
					]
				},
				email: {
					rules: [
						{ required: true, errorMessage: '请输入邮箱', },
						{ format: 'email', errorMessage: '邮箱格式错误' },
					]
				},
				unit: {
					rules: [
						{ required: true, errorMessage: '请输入工作单位', },
					]
				},
				protocolId: {
					rules: [
						{ required: true, errorMessage: '请先阅读并同意协议', },
					]
				},
			},
		};
	},
	methods: {
		navigateBack() {
			uni.navigateBack();
		},

		addressChange(e) {
			this.formData.addressName = e.detail.value[e.detail.value.length - 1].text;
		},

		genderChange(e) {
			this.formData.genderName = e.detail.data.text;
		},

		politicsChange(e) {
			this.polIndex = e.detail.value;
			this.formData.politics = this.polData[e.detail.value];
		},

		protocolChange(e) {
			this.formData.protocolName = this.proData[e.detail.value];
		},

		submit() {
			this.$refs.form.validate().then(res=>{
				console.log('表单数据信息：', res);
			}).catch(err =>{
				console.log('表单错误信息：', err);
			})
		}
	},
};
</script>

<style scoped>
	.wrapper{
		width: 100vw;
		min-height: 100vh;
		background-color: #f6f6f6;
	}
	.container{
		margin: 10px;
		padding: 0 15px;
		background: #FFFFFF;
		box-shadow: 0px 0px 9px 0px rgba(194, 194, 194, 0.08);
		border-radius: 5px;
	}
	.label{
		font-size: 12px;
		font-weight: 400;
		color: #333333;
		padding: 25px 0 0 0;
	}
	.text{
		font-size: 15px;
		font-weight: 400;
		color: #333333;
		padding: 15px 0 0;
	}

	.right_text {
		float: right;
		margin-top: -20px;
		color: #2EB3A8;
		font-size: 12px;
	}

</style>
