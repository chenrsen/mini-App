<template>
	<view class="wrapper">
		<view class="navigationBar">
			<uni-nav-bar fixed title="" left-width="80vw" right-width="16vw" right-text="">
				<block slot="left">
					<view class="navigationBar-leftText">中国能源研究会综合能源服务专委会</view>
				</block>
				<block slot="right">
					<navigator url="/subPackages/member/join/index">
						<view class="">加入会员</view>
					</navigator>
				</block>
			</uni-nav-bar>
		</view>
		<navigator url="/subPackages/common/search/index">
			<view class="searchBarContainer">
				<uni-search-bar
					placeholder="请输入关键词搜索"
					bgColor="#F5F5F5"
					:radius="23"
					@confirm="search"
					@input="input"
				></uni-search-bar>
			</view>
		</navigator>
		<view class="tabs">
			<view
				v-for="(tab, index) in tabs.list"
				:key="index"
				class="tabs-item"
				:class="tabs.activeIndex === index ? 'active' : ''"
				:data-index="index"
				@click="tabOnTap"
			>
				{{ tab.title }}
			</view>
		</view>
		<view class="container">
			<keep-alive>
				<template v-if="tabs.activeIndex === 0">
					<Home />
				</template>
				<template v-else-if="tabs.activeIndex === 1">
					<Intro />
				</template>
				<template v-else-if="tabs.activeIndex === 2">
					<News />
				</template>
			</keep-alive>
		</view>
	</view>
</template>

<script>
import Home from './components/Home.vue';
import Intro from './components/Intro.vue';
import News from './components/News.vue';
export default {
	components: {
		Home,
		Intro,
		News,
	},
	data() {
		return {
			tabs: {
				list: [
					{
						title: '首页',
					},
					{
						title: '专委会',
					},
					{
						title: '新闻',
					},
					{
						title: '服务',
					},
				],
				activeIndex: 0,
			},
		};
	},
	methods: {
		tabOnTap(e) {
			const { index } = e.currentTarget.dataset;
			if (this.tabs.activeIndex === index) return;
			this.tabs.activeIndex = index;
		},
		focusOnChange(e) {
			this.focus.activeIndex = e.detail.current;
		},
	},
};
</script>

<style scoped>
.wrapper {
	background-color: #f6f6f6;
	min-height: 100vh;
	padding-bottom: 40px;
	box-sizing: border-box;
}
.navigationBar {
	border-bottom: 1px solid #dadada;
}
.navigationBar-leftText {
	font-size: 16px;
	font-weight: bold;
	color: #333333;
	line-height: 23px;
}
.searchBarContainer {
	width: 100vw;
	background-color: #fff;
	box-shadow: 0px 1px 9px 0px rgba(60, 60, 60, 0.18);
	pointer-events: none;
}
.tabs {
	width: 100vw;
	height: 42px;
	display: flex;
}
.tabs-item {
	flex: 1;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 13px;
	font-weight: 400;
	color: #333333;
}
.tabs-item.active {
	color: #2eb3a8;
}
.container {
	margin: 0 10px;
}
</style>
