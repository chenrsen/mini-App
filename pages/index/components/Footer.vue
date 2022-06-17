<template>
	<view>
		<view class="footer">
			<view class="footer-info">
				<text class="footer-info-text">地址：北京市西城区南横东街8号都城大厦17层</text>
				<text class="footer-info-text">邮编：100052</text>
				<text class="footer-info-text">邮箱：zhnyfw@cers.org.cn</text>
				<text class="footer-info-text">电话：010-63505064</text>
			</view>
			<view class="footer-qrcode">
				<image class="footer-qrcode-img"></image>
				<text class="footer-qrcode-text">微信公众号</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {};
</script>

<style scoped>
.footer {
	padding: 6px 15px;
	background-color: #fff;
	border-radius: 5px;
	display: flex;
	justify-content: space-between;
}
.footer-info {
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	align-items: flex-start;
}
.footer-info-text {
	font-size: 10px;
	font-weight: 400;
	color: #333333;
	margin: 6px 0;
	line-height: 1;
}
.footer-qrcode {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}
.footer-qrcode-img {
	width: 74px;
	height: 74px;
	background-color: rgba(0, 0, 0, 0.1);
}
.footer-qrcode-text {
	font-size: 10px;
	font-weight: 400;
	color: #333333;
}
</style>
