<template>
	<view>
		<view class="focusContainer">
			<uni-swiper-dot
				:info="focus.list"
				mode="dot"
				:current="focus.activeIndex"
				:dotsStyles="focus.dotsStyles"
			>
				<swiper class="focus" circular @change="focusOnChange">
					<swiper-item v-for="(item, index) in focus.list" :key="index">
						<navigator
							:url="item.navigateUrl"
							class="focus-item"
							:style="'background:' + item.bg + ';'"
						></navigator>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
		</view>
		<view class="entry">
			<navigator
				v-for="(item, index) in entry.list"
				:key="index"
				:url="item.navigateUrl"
				class="entry-item"
				:style="'background:' + item.bg + ';'"
			></navigator>
		</view>
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
			<view class="news" v-if="tabs.activeIndex >= 0">
				<template v-for="(item, index) in tabs.list[tabs.activeIndex].data.list">
					<navigator :key="index" :url="item.navigateUrl" class="news-item">
						<view class="news-item-title">{{ item.title }}</view>
						<view class="news-item-date">{{ item.date }}</view>
					</navigator>
					<template v-if="index !== tabs.list[tabs.activeIndex].data.list.length - 1">
						<view class="news-item-line"></view>
					</template>
				</template>
				<view class="news-loadMoreContainer"><button class="news-loadMore">查看更多</button></view>
			</view>
		</view>
		<view class="info">
			<navigator
				v-for="(item, index) in info.list"
				:key="index"
				:url="item.navigateUrl"
				class="info-item"
			>
				<image :src="item.icon" class="info-item-icon"></image>
				<text class="info-item-title">{{ item.title }}</text>
			</navigator>
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
			focus: {
				list: [
					{
						bg: 'rgba(255,0,0,0.1)',
						navigateUrl: '/subPackages/common/search/index',
					},
					{
						bg: 'rgba(0,255,0,0.1)',
						navigateUrl: '/subPackages/common/search/index',
					},
					{
						bg: 'rgba(0,0,255,0.1)',
						navigateUrl: '',
					},
				],
				activeIndex: 0,
				dotsStyles: {
					bottom: 7,
					backgroundColor: 'rgba(0,0,0,0.3)',
					selectedBackgroundColor: '#fff',
					border: 'none',
					selectedBorder: 'none',
				},
			},
			entry: {
				list: [
					{
						bg: 'rgba(255,0,0,0.1)',
						navigateUrl: '/subPackages/common/search/index',
					},
					{
						bg: 'rgba(0,255,0,0.1)',
						navigateUrl: '/subPackages/common/search/index',
					},
				],
			},
			tabs: {
				list: [
					{
						title: '学会动态',
						data: {
							list: new Array(5).fill({
								title: '学会动态中国科协束为书记一行莅临中国中国科协束为书记一行莅临中国',
								date: '2022-03-05',
								navigateUrl: '/subPackages/common/search/index',
							}),
						},
					},
					{
						title: '政策研究',
						data: {
							list: new Array(5).fill({
								title: '政策研究中国科协束为书记一行莅临中国中国科协束为书记一行莅临中国',
								date: '2022-03-05',
								navigateUrl: '/subPackages/common/search/index',
							}),
						},
					},
					{
						title: '行业要闻',
						data: {
							list: new Array(5).fill({
								title: '行业要闻中国科协束为书记一行莅临中国中国科协束为书记一行莅临中国',
								date: '2022-03-05',
								navigateUrl: '/subPackages/common/search/index',
							}),
						},
					},
				],
				activeIndex: -1,
				underline: {
					left: -100,
					inited: false,
				},
			},
			info: {
				list: [
					{
						icon: require('@/static/index/icon1.png'),
						title: '组织介绍',
						navigateUrl: '/subPackages/common/search/index',
					},
					{
						icon: require('@/static/index/icon2.png'),
						title: '工作章程',
						navigateUrl: '/subPackages/common/search/index',
					},
					{
						icon: require('@/static/index/icon3.png'),
						title: '委员名单',
						navigateUrl: '/subPackages/common/search/index',
					},
				],
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
		focusOnChange(e) {
			this.focus.activeIndex = e.detail.current;
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
.news-item {
	padding: 0 10px;
	height: 48px;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.news-item-title {
	max-width: 180px;
	font-size: 11px;
	font-weight: 400;
	color: #666666;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	margin-left: 10px;
}
.news-item-date {
	font-size: 12px;
	font-weight: 400;
	color: #999999;
	margin-right: 6px;
}
.news-item-line {
	height: 1px;
	background: #e7e7e7;
	margin: 0 10px;
}
.news-loadMoreContainer {
	width: 100%;
	height: 54px;
	display: flex;
	align-items: center;
	justify-content: center;
}
.news-loadMore {
	width: 114px;
	height: 29px;
	background: #00b6a8;
	border-radius: 3px;
	font-size: 12px;
	font-weight: 400;
	color: #ffffff;
	line-height: 29px;
}
.info {
	display: flex;
	justify-content: space-between;
	padding: 0 10px;
	margin-top: 17px;
}
.info-item {
	width: 54px;
	height: 74px;
	display: flex;
	flex-direction: column;
	align-items: auto;
	justify-content: space-between;
}
.info-item-icon {
	width: 54px;
	height: 54px;
}
.info-item-title {
	font-size: 11px;
	font-weight: 400;
	color: #333333;
	text-align: center;
}
.footerContainer {
	margin-top: 14px;
}
</style>
