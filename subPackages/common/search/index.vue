<template>
	<view class="wrapper">
		<uni-nav-bar
			fixed
			left-icon="left"
			left-width="30px"
			right-width="0px"
			@clickLeft="navigateBack"
		>
			<view style="width:100%;display:flex;align-items:center;">
				<view v-slot:default style="flex:1;">
					<uni-search-bar
						placeholder="请输入关键词搜索"
						bgColor="#F5F5F5"
						:radius="23"
						cancelButton="always"
						@confirm="search"
						@input="input"
					></uni-search-bar>
				</view>
			</view>
		</uni-nav-bar>
		<view class="section">
			<view class="section-header">
				<text class="section-header-title">搜索历史</text>
				<uni-icons type="trash" color="#999" size="20"></uni-icons>
			</view>
			<view class="section-body">
				<view v-for="(item, index) in history" :key="item" class="label">{{ item }}</view>
			</view>
		</view>
		<view class="section">
			<view class="section-header"><text class="section-header-title">搜索推荐</text></view>
			<view class="section-body">
				<view v-for="(item, index) in recommend" :key="item" class="label">{{ item }}</view>
			</view>
		</view>
		<view class="section">
			<view class="section-header"><text class="section-header-title">热门搜索</text></view>
			<view class="section-body hot">
				<view v-for="(item, index) in hot" :key="item" class="hot-item">
					<view class="hot-item-rank">{{ index + 1 }}</view>
					<view class="hot-item-title">{{ item }}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			history: new Array(4).fill(1).map((e, i) => `标签${i + 1}`),
			recommend: new Array(8).fill(1).map((e, i) => `标签${i + 1}`),
			hot: new Array(8)
				.fill(1)
				.map((e, i) => `${i + 1}热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜热搜`),
		};
	},
	methods: {
		navigateBack() {
			uni.navigateBack();
		},

		search(e) {
			console.log(e);
		},

		input(value) {
			console.log(value);
		},
	},
};
</script>

<style scoped>
.wrapper {
	width: 100vw;
	min-height: 100vh;
}

.section {
	padding: 13px 20px 5px;
}
.section-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.section-header-title {
	font-size: 14px;
	font-weight: 400;
	color: #333333;
}
.section-body {
	margin-top: 3px;
	display: flex;
	flex-wrap: wrap;
}
.label {
	padding: 0 15px;
	height: 25px;
	line-height: 25px;
	font-size: 12px;
	font-weight: 400;
	color: #999999;
	border: 1px solid #e6e6e6;
	margin-right: 15px;
	margin-top: 10px;
}
.section-body.hot {
	flex-direction: column;
}
.hot-item {
	width: 100%;
	height: 48px;
	display: flex;
	align-items: center;
	justify-content: center;
	border-bottom: 1px solid #e7e7e7;
}
.hot-item-rank {
	width: 13px;
	height: 13px;
	line-height: 13px;
	text-align: center;
	font-size: 12px;
	font-weight: 400;
	color: #fffefe;
	border-radius: 1px;
	background: linear-gradient(0deg, #d0d0d0, #959595);
	margin-right: 9px;
}
.hot-item-title{
	flex: 1;
	font-size: 12px;
	font-weight: 400;
	color: #333333;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.hot-item:nth-child(1) .hot-item-rank {
	background: linear-gradient(0deg, #9e0000, #ff0000);
}
.hot-item:nth-child(2) .hot-item-rank {
	background: linear-gradient(0deg, #ff6000, #ffae00);
}
.hot-item:nth-child(3) .hot-item-rank {
	background: linear-gradient(0deg, #e4b600, #e7d406);
}

/* deep */
.wrapper::v-deep .uni-navbar__header-container {
	padding: 0;
}
.wrapper::v-deep .uni-searchbar {
	padding: 0;
	display: flex;
	align-items: center;
}
.wrapper::v-deep .uni-searchbar__box {
	height: 33px;
}
</style>
