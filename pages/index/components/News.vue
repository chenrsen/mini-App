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
			<view class="news" v-if="tabs.activeIndex >= 0">
				<!-- <view class="news_cont fir_cont">
					<view class="content_view fir_con_left">
						<view class="left_con">
							<text class="fir_con_text">中国国家电网有限公司与丹麦国家电网</text>
							<text class="fir_con_text">公司签署合作协议</text>
						</view>
						<view class="left_sec_con">
							<view class="sec_con_text">
								<text class="fir_con_text">2022-03-05</text>
							</view>
							<view class="sec_con_img">
								<image src="@/static/heart@2x.png" class="fir_con_img"></image>
								<image src="@/static/info@2x.png" class="fir_con_img"></image>
								<image src="@/static/forwarding@2x.png" class="fir_con_img"></image>
							</view>
						</view>
					</view>
					<view class="content_view">
						<image class="right_con_img"></image>
					</view>
				</view>
				<uni-view class="news-item-line"></uni-view>
				
				<view class="news_cont sec_cont">
					<view class="cont_one">
						<text class="fir_con_text">国家电网两项特高压工程开工，总投资109亿元</text>
					</view>
					<view class="cont_two">
						<image class="cont_img"></image>
						<image class="cont_img"></image>
						<image class="cont_img"></image>
					</view>
					<view class="cont_three">
						<view class="left_sec_con">
							<view class="sec_con_text">
								<text class="fir_con_text">2022-03-05</text>
							</view>
							<view class="cont_bot_img">
								<image src="@/static/heart@2x.png" class="fir_con_img"></image>
								<image src="@/static/info@2x.png" class="fir_con_img"></image>
								<image src="@/static/forwarding@2x.png" class="fir_con_img"></image>
							</view>
						</view>
					</view>
				</view>
				<uni-view class="news-item-line"></uni-view>
				
				<view class="news_cont thr_cont">
					<view class="cont_one">
						<text class="fir_con_text">国家电网董事长辛保安与中国石化董事长马永生会谈</text>
					</view>
					<view class="cont_two">
						<video src=""  class="cont_video" controls></video>
					</view>
					<view class="cont_three">
						<view class="left_sec_con">
							<view class="sec_con_text">
								<text class="fir_con_text">2022-03-05</text>
							</view>
							<view class="cont_bot_img">
								<image src="@/static/heart@2x.png" class="fir_con_img"></image>
								<image src="@/static/info@2x.png" class="fir_con_img"></image>
								<image src="@/static/forwarding@2x.png" class="fir_con_img"></image>
							</view>
						</view>
					</view>
				</view>
				<uni-view class="news-item-line"></uni-view> -->
				<template v-for="(item, index) in tabs.list[tabs.activeIndex].data.list">
					<view :key="index">
						<view class="news_cont fir_cont">
							<view class="content_view fir_con_left">
								<view class="left_con">
									<template v-for="(f, tIndex) in item.fir_list">
										<text class="fir_con_text" :key="tIndex">{{f}}</text>
									</template>
								</view>
								<view class="left_sec_con">
									<view class="sec_con_text">
										<text class="fir_con_text">{{item.fir_time}}</text>
									</view>
									<view class="sec_con_img">
										<template v-for="(url, iIndex) in item.fir_img">
											<image class="fir_con_img" :src="url" :key="iIndex" />
										</template>
									</view>
								</view>
							</view>
							<view class="content_view">
								<image class="right_con_img"></image>
							</view>
						</view>
						<uni-view class="news-item-line"></uni-view>
						
						<view class="news_cont sec_cont">
							<view class="cont_one">
								<text class="fir_con_text">{{item.sec_text}}</text>
							</view>
							<view class="cont_two">
								<template v-for="(url, iIndex) in item.secImgList">
									<image class="cont_img" :src="url" :key="iIndex" />
								</template>
							</view>
							<view class="cont_three">
								<view class="left_sec_con">
									<view class="sec_con_text">
										<text class="fir_con_text">{{item.sec_time}}</text>
									</view>
									<view class="cont_bot_img">
										<template v-for="(url, iIndex) in item.sec_img">
											<image class="fir_con_img" :src="url" :key="iIndex" />
										</template>
									</view>
								</view>
							</view>
						</view>
						<uni-view class="news-item-line"></uni-view>
						
						<view class="news_cont thr_cont">
							<view class="cont_one">
								<text class="fir_con_text">{{item.thr_text}}</text>
							</view>
							<view class="cont_two">
								<video :src="item.thr_video"  class="cont_video" controls></video>
							</view>
							<view class="cont_three">
								<view class="left_sec_con">
									<view class="sec_con_text">
										<text class="fir_con_text">{{item.thr_time}}</text>
									</view>
									<view class="cont_bot_img">
										<template v-for="(url, iIndex) in item.thr_img">
											<image class="fir_con_img" :src="url" :key="iIndex" />
										</template>
									</view>
								</view>
							</view>
						</view>
						<uni-view class="news-item-line"></uni-view>
					</view>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			tabs: {
				list: [
					{
						title: '学会动态',
						data: {
							list: new Array(1).fill({
								fir_list: ['学会动态 中国国家电网有限公司与丹麦国家电网公司签署合作协议'],
								fir_time: '2022-04-20',
								fir_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								sec_text: '国家电网两项特高压工程开工，总投资109亿元',
								secImgList: ['', '', ''],
								sec_time: '2022-04-20',
								sec_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								thr_text: '国家电网董事长辛保安与中国石化董事长马永生会谈',
								thr_video: '',
								thr_time: '2022-04-20',
								thr_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
							}),
						},
					},
					{
						title: '政策研究',
						data: {
							list: new Array(3).fill({
								fir_list: ['政策研究 中国国家电网有限公司与丹麦国家电网公司签署合作协议'],
								fir_time: '2022-04-21',
								fir_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								sec_text: '国家电网两项特高压工程开工，总投资109亿元',
								secImgList: ['', '', ''],
								sec_time: '2022-04-21',
								sec_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								thr_text: '国家电网董事长辛保安与中国石化董事长马永生会谈',
								thr_video: '',
								thr_time: '2022-04-21',
								thr_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
							}),
						},
					},
					{
						title: '行业要闻',
						data: {
							list: new Array(5).fill({
								fir_list: ['行业要闻 中国国家电网有限公司与丹麦国家电网公司签署合作协议'],
								fir_time: '2022-04-22',
								fir_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								sec_text: '国家电网两项特高压工程开工，总投资109亿元',
								secImgList: ['', '', ''],
								sec_time: '2022-04-22',
								sec_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
								thr_text: '国家电网董事长辛保安与中国石化董事长马永生会谈',
								thr_video: '',
								thr_time: '2022-04-22',
								thr_img: [require('@/static/heart@2x.png'), require('@/static/info@2x.png'), require('@/static/forwarding@2x.png')],
							}),
						},
					},
				],
				activeIndex: -1,
				underline: {
					left: -100,
					inited: false,
				},
			}};
	},
	mounted() {
		// fetch
		// console.log('fetch');
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

.news_cont {
	padding: 6px 15px;
	background-color: #fff;
	border-radius: 5px;
	display: flex;
	justify-content: space-between;
}

.sec_cont, .thr_cont {
	flex-direction: column;
}

.cont_two {
	display: flex;
	flex-direction: row;
}

.content_view, .left_con {
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	align-items: flex-start;
}

.fir_con_left {
	width: 60%;
}

.left_sec_con {
	width: 100%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}

.sec_con_img {
	width: 30%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}

.fir_con_text {
	font-size: 10px;
	font-weight: 400;
	color: #333333;
	margin: 6px 0;
	line-height: 1;
}
.fir_con_img {
	width: 14px;
	height: 12px;
}
.right_con_img {
	width: 74px;
	height: 74px;
	background-color: rgba(0, 0, 0, 0.1);
}

.cont_img {
	width: 100px;
	height: 80px;
	margin: 0 5px;
	background-color: rgba(0, 0, 0, 0.1);
}

.cont_bot_img {
	width: 20%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}

.cont_video {
	width: 100%;
	height: 130px;
}
</style>
