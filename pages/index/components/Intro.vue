<template>
	<view>
		<view class="container">
			<view class="tabs">
				<view
					ref="tabsItems"
					v-for="(tab, index) in tabs.list"
					:key="index"
					class="tabs-item"
					:class="tabs.activeIndex === index ? 'active' : ''"
					:data-index="index"
					@click="tabOnTap"
				>
					{{ tab.title }}
				</view>
				<view
					ref="tabsUnderline"
					class="tabs-underline"
					:class="this.tabs.underline.inited ? 'inited' : ''"
					:style="'transform: translateX(' + tabs.underline.left + 'px);'"
				/>
			</view>
			<template v-if="tabs.activeIndex === 0">
				<view class="brief">
					<image class="brief-thumb"></image>
					<text class="brief-title">{{ intro.title }}</text>
					<text class="brief-desc">{{ intro.desc }}</text>
				</view>
			</template>
			<template v-else-if="tabs.activeIndex === 1">
				<view class="document">工作章程详情...</view>
			</template>
			<template v-else-if="tabs.activeIndex === 2">
				<view class="member">
					<template v-for="(item, index) in intro.memberList">
						<view :key="index" class="member-item">
							<view class="member-item-title">{{ item.title }}</view>
							<view style="display: flex;">
								<view
									v-for="(name, index) in item.name"
									:key="index"
									class="member-item-name"
								>
									<navigator :url="'/subPackages/member/list/index?name=' + encodeURIComponent(JSON.stringify(name))">
										{{ name }}
									</navigator>
								</view>
							</view>
						</view>
						<template v-if="index !== intro.memberList.length - 1">
							<view class="member-item-line"></view>
						</template>
					</template>
				</view>
			</template>
		</view>
		<view class="footerContainer"><Footer /></view>
	</view>
</template>

<script>
import Footer from './Footer.vue';
export default {
	components: {
		Footer,
	},
	data() {
		return {
			intro: {
				thumb: '',
				title: '综合能源服务专委会简介',
				desc:
					'为促进综合能源服务专业领域高质量发展，推动“四个革命、一个合作”能源安全新战略落地，2021年8月30日，中国能源研究会正式批准成立中国能源研究会综合能源服务专业委员会（以下简称“综合能源服务专委会”）。综合能源服务专委会将助力综合能源行业释放优质产能，推动能源安全稳定供应，同时为能源行业提供多方位优质服务，助力实现“双碳”目标。',
				document: {}, // 工作章程
				memberList: [
					{
						title: '主任',
						name: ['李明'],
					},
					{
						title: '顾问',
						name: ['陈清泉'],
					},
					{
						title: '主任委员',
						name: ['刘吉臻'],
					},
					{
						title: '常务副主任委员',
						name: ['任伟理'],
					},
					{
						title: '副主任委员',
						name: ['王成山'],
					},
					{
						title: '秘书长',
						name: ['杨旭升'],
					},
					{
						title: '副秘书长',
						name: ['代红才'],
					},
					{
						title: '委员',
						name: ['于德翔', '王宏安', '王维洲', '文劲宇', '艾芊'],
					},
				],
			},
			tabs: {
				list: [
					{
						title: '组织简介',
					},
					{
						title: '工作章程',
					},
					{
						title: '委员名录',
					},
				],
				activeIndex: -1,
				underline: {
					left: -100,
					inited: false,
				},
			},
		};
	},
	mounted() {
		// fetch
		console.log('fetch');
		this.switchTab(0);
	},
	methods: {
		tabOnTap(e) {
			const { index } = e.currentTarget.dataset;
			if (this.tabs.activeIndex === index) return;
			this.switchTab(index);
		},
		switchTab(index) {
			this.tabs.activeIndex = index;
			this.$nextTick(function() {
				const { left, width: itemWidth } = this.$refs.tabsItems[
					this.tabs.activeIndex
				].$el.getBoundingClientRect();
				const { width: lineWidth } = this.$refs.tabsUnderline.$el.getBoundingClientRect();

				this.tabs.underline.left = left + (itemWidth - lineWidth) / 2;
				if (!this.tabs.underline.inited) this.tabs.underline.inited = true;
			});
		},
	},
};
</script>

<style scoped>
.focus {
	width: 355px;
	height: 134px;
	border-radius: 5px;
	overflow: hidden;
}
.focus-item {
	width: 100%;
	height: 100%;
	background-size: 100% auto;
	background-repeat: no-repeat;
	background-position: center;
}
.entry {
	margin: 5px 0 0;
	display: flex;
	justify-content: space-between;
}
.entry-item {
	flex: 1;
	height: 60px;
	border-radius: 5px;
	margin-right: 5px;
}
.entry-item:last-child {
	margin-right: 0;
}
.container {
	margin-top: 5px;
	background-color: #fff;
	border-radius: 5px;
}
.tabs {
	height: 28px;
	display: flex;
	border-bottom: 1px solid #e7e7e7;
	position: relative;
}
.tabs-item {
	padding: 0 8px;
	height: 28px;
	line-height: 28px;
	font-size: 13px;
	font-weight: 400;
	color: #666666;
}
.tabs-item.active {
	color: #2eb3a8;
}
.tabs-underline {
	position: absolute;
	bottom: -1px;
	left: -10px;
	width: 18px;
	height: 1px;
	background: #2eb3a8;
	opacity: 0;
	transition: opacity 2s, transform 0.3s;
}
.tabs-underline.inited {
	opacity: 1;
}
.brief {
	padding: 20px;
	display: flex;
	flex-direction: column;
	align-items: center;
}
.brief-thumb {
	width: 315px;
	height: 166px;
	background-color: rgba(0, 0, 0, 0.1);
	border-radius: 5px;
}
.brief-title {
	font-size: 15px;
	font-weight: 500;
	color: #333333;
	margin-top: 35px;
}
.brief-desc {
	font-size: 14px;
	font-weight: 400;
	color: #666666;
	text-indent: 30px;
	text-align: justify;
	margin-top: 20px;
}
.document {
	padding: 20px;
}
.member {
	padding: 0 10px;
}
.member-item {
	width: 100%;
	height: 47px;
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.member-item-title {
	font-size: 12px;
	font-weight: 400;
	color: #333333;
	margin-left: 7px;
	margin-right: 3px;
}
.member-item-name {
	font-size: 12px;
	font-weight: 400;
	color: #999999;
	margin-left: 12px;
}
.member-item-line {
	height: 1px;
	background: #e7e7e7;
}
.footerContainer {
	margin-top: 14px;
}
</style>
