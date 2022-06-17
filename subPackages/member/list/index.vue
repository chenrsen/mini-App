<template>
	<view class="wrapper">
		<uni-nav-bar fixed left-icon="left" @clickLeft="navigateBack" title="委员名录"></uni-nav-bar>
		<view class="focus">
			<z-swiper v-model="list" :options="options" @slideChange="focusOnChange">
				<z-swiper-item :custom-style="{width:'70vw',height:'48vw'}" v-for="(item,index) in list" :key="index">
					<image class="avator" mode="aspectFill" />
				</z-swiper-item>
			</z-swiper>
		</view>
		<view class="container">
			<view class="name">{{list[activeIndex].name}}</view>
			<view class="desc">{{list[activeIndex].desc}}</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			options: {
				effect: 'coverflow',
				centeredSlides: true,
				slidesPerView: 'auto',
				coverflowEffect: {
					rotate: 50,
					stretch: 0,
					depth: 100,
					modifier: 1,
					slideShadows: true,
				},
			},
			list: new Array(5).fill(1).map((e, i) => {
				return {
					// avator: `https://cdn.zebraui.com/zebra-ui/images/swipe-demo/swipe${i + 1}.jpg`,
					name: `${i + 1}刘吉臻`,
					desc: `${i + 1} 2013年11月15日公布的《中共中央关于全面深化改革若干重大问题的决定》中，明确要求改革院士遴选和管理体制，优化学科布局，提高中青年人才比例，实行院士退休和退出制度。2021年中国科学院院士增选结果于2021年11月18日揭晓，共有149人当选。其中，中国科学院增选院士65人，中国工程院增选院士84人。`,
				}
			}),
			activeIndex: 0,
		};
	},
	methods: {
		navigateBack() {
			uni.navigateBack();
		},
		focusOnChange(swiper){
			if(this.activeIndex === swiper.activeIndex) return;
			this.activeIndex = swiper.activeIndex;
		},

		onLoad: function (option) {
			console.log(JSON.parse(decodeURIComponent(option.name)));
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
	.focus{
		width: 100vw;
		height: 200px;
		display: flex;
		align-items: center;
	}
	.avator{
		width: 260px;
		height: 177px;
		border-radius: 5px;
		background-color: rgba(0,0,0,0.1);
	}
	.container{
		margin: 10px;
		padding: 10px;
		background-color: #fff;
		border-radius: 5px;
	}
	.name{
		font-size: 18px;
		font-weight: 400;
		color: #333333;
		text-align: center;
	}
	.desc{
		font-size: 10px;
		font-weight: 400;
		color: #666666;
		text-align: justify;
		margin-top: 12px;
	}
	
</style>
