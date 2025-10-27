<template>
	<view class="index-page">
		<!-- 顶部标题栏 -->
		<view class="header">
			<view class="title">24小时自助情趣成人用品商城</view>
			<view class="search-bar" @click="goToSearch">

				<image class="icon" src="../../static/search.png" mode="widthfix"></image>
				<text class="search-placeholder">搜索商品</text>
			</view>
		</view>

		<!-- 主横幅 -->
		<view class="banner">
			<view class="banner-content">
				<view class="banner-top">
					<view class="love-text">Love</view>
					<view class="heart-icon">💖</view>
					<view class="recommend-text">
						<view class="crown-icon">🏆</view>
						<text>趣网好物榜</text>
						<text>荐你所想</text>
					</view>
				</view>
				<view class="banner-title">亲密交流装备</view>
				<view class="banner-button">用「行动」表达爱</view>
			</view>
		</view>

		<!-- 商品分类 -->
		<view class="category-section">
			<view class="category-item" v-for="(item, index) in categories" :key="index" @click="goToCategory(item)">
				<view class="category-icon" :style="{ backgroundColor: item.color }">
					<text class="icon-text">{{ item.icon }}</text>
				</view>
				<text class="category-name">{{ item.name }}</text>
			</view>
		</view>

		<!-- 排行榜 -->
		<view class="ranking-section">
			<view class="section-header">
				<view class="section-title">
					<view class="red-dot"></view>
					<text>排行榜</text>
				</view>
				<text class="section-subtitle">诚意推荐品质商品</text>
				<text class="more-link">更多></text>
			</view>
			<scroll-view class="ranking-scroll" scroll-x="true">
				<view class="ranking-list">
					<view class="ranking-item" v-for="(item, index) in rankingProducts" :key="index">
						<view class="ranking-badge">{{ index + 1 }}</view>
						<view class="product-image">
							<image :src="item.image" mode="aspectFill"></image>
						</view>
						<view class="product-info">
							<view class="hot-tag">热度TOP {{ index + 1 }}</view>
							<text class="product-name">{{ item.name }}</text>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>

		<!-- 新品推荐 -->
		<view class="new-products-section">
			<view class="section-header">
				<view class="section-title">
					<view class="red-dot"></view>
					<text>首发新品</text>
				</view>
				<text class="section-subtitle">新品推荐</text>
				<text class="more-link">更多></text>
			</view>
			<view class="new-products-list">
				<view class="new-product-item" v-for="(item, index) in newProducts" :key="index">
					<view class="product-image">
						<image :src="item.image" mode="aspectFill"></image>
					</view>
					<view class="product-info">
						<text class="product-name">{{ item.name }}</text>
						<text class="product-desc">{{ item.description }}</text>
					</view>
					<!-- <view class="product-action">
                        <view class="action-icon" v-if="index === 0">🏠</view>
                        <view class="action-icon" v-else>🛒</view>
                        <text class="action-text">{{ index === 0 ? '下单页' : '购物车' }}</text>
                    </view> -->
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				categories: [{
						name: '男性用品',
						icon: '♂️',
						color: '#FF6B6B'
					},
					{
						name: '女性用品',
						icon: '♀️',
						color: '#9B59B6'
					},
					{
						name: '飞机杯',
						icon: '🥤',
						color: '#3498DB'
					},
					{
						name: '润滑液',
						icon: '💧',
						color: '#F39C12'
					},
					{
						name: '避孕套',
						icon: '🛡️',
						color: '#2ECC71'
					}
				],
				rankingProducts: [{
						name: '名流避孕套持...',
						image: '/static/images/product1.jpg'
					},
					{
						name: '杜丝邦情趣震...',
						image: '/static/images/product2.jpg'
					},
					{
						name: '万孚 艾滋病检...',
						image: '/static/images/product3.jpg'
					},
					{
						name: '名流避孕套持...',
						image: '/static/images/product1.jpg'
					},
					{
						name: '杜丝邦情趣震...',
						image: '/static/images/product2.jpg'
					},
					{
						name: '万孚 艾滋病检...',
						image: '/static/images/product3.jpg'
					}
				],
				newProducts: [{
						name: '血唾二合一检测',
						description: 'ACCUR GEASY 防漏检专利技术',
						image: '/static/images/new1.jpg'
					},
					{
						name: 'HIV 1/2检测',
						description: '雅培 Abbott 线下同款 现货速发',
						image: '/static/images/new2.jpg'
					},
					{
						name: '血唾二合一检测',
						description: 'ACCUR GEASY 防漏检专利技术',
						image: '/static/images/new1.jpg'
					},
					{
						name: 'HIV 1/2检测',
						description: '雅培 Abbott 线下同款 现货速发',
						image: '/static/images/new2.jpg'
					},
					{
						name: '血唾二合一检测',
						description: 'ACCUR GEASY 防漏检专利技术',
						image: '/static/images/new1.jpg'
					},
					{
						name: 'HIV 1/2检测',
						description: '雅培 Abbott 线下同款 现货速发',
						image: '/static/images/new2.jpg'
					}
				]
			}
		},

		// 首页搜索跳转第二首
		methods: {
			goToSearch() {
				uni.navigateTo({
					url: '/pages/search/search'
				})
			},
			goToCategory(item) {
				uni.navigateTo({
					url: `/pages/category/category?type=${item.name}`
				})
			}
		}
	}
</script>

<style scoped>
	.index-page {
		background-color: #F8F8F8;
		min-height: 100vh;
	}

	/* 顶部标题栏 */
	.header {
		background: linear-gradient(135deg, #FF69B4, #FF1493);
		padding: 20rpx 30rpx 30rpx;
		color: white;
	}

	.title {
		font-size: 32rpx;
		font-weight: bold;
		text-align: center;
		margin-bottom: 20rpx;
	}

	.search-bar {
		background-color: rgba(255, 255, 255, 0.9);
		border-radius: 45rpx;
		padding: 20rpx 30rpx;
		display: flex;
		align-items: center;
		color: #999;
	}

	.search-icon {
		margin-right: 15rpx;
		font-size: 28rpx;
	}

	.search-placeholder {
		font-size: 28rpx;
		color: #999;
	}

	/* 主横幅 */
	.banner {
		background: linear-gradient(135deg, #4A148C, #7B1FA2);
		margin: 20rpx 30rpx;
		border-radius: 20rpx;
		padding: 40rpx 30rpx;
		position: relative;
		overflow: hidden;
	}

	.banner::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: linear-gradient(45deg, transparent 30%, rgba(255, 255, 255, 0.1) 50%, transparent 70%);
		animation: shimmer 3s infinite;
	}

	@keyframes shimmer {
		0% {
			transform: translateX(-100%);
		}

		100% {
			transform: translateX(100%);
		}
	}

	.banner-content {
		position: relative;
		z-index: 1;
	}

	.banner-top {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 20rpx;
	}

	.love-text {
		font-size: 36rpx;
		font-weight: bold;
		color: #FF69B4;
		font-style: italic;
	}

	.heart-icon {
		font-size: 24rpx;
		margin-left: 10rpx;
	}

	.recommend-text {
		display: flex;
		align-items: center;
		font-size: 24rpx;
		color: #FFD700;
	}

	.crown-icon {
		margin-right: 10rpx;
		font-size: 20rpx;
	}

	.banner-title {
		font-size: 48rpx;
		font-weight: bold;
		color: #FF69B4;
		text-align: center;
		margin: 30rpx 0;
		text-shadow: 0 0 20rpx rgba(255, 105, 180, 0.5);
	}

	.banner-button {
		background: linear-gradient(90deg, #00BFFF, #1E90FF);
		color: white;
		padding: 20rpx 40rpx;
		border-radius: 50rpx;
		text-align: center;
		font-size: 28rpx;
		font-weight: bold;
		box-shadow: 0 4rpx 20rpx rgba(0, 191, 255, 0.3);
		border: 2rpx solid rgba(255, 255, 255, 0.3);
	}

	/* 商品分类 */
	.category-section {
		display: flex;
		justify-content: space-around;
		padding: 40rpx 30rpx;
		background-color: white;
		margin: 20rpx 30rpx;
		border-radius: 20rpx;
		box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
	}

	.category-item {
		display: flex;
		flex-direction: column;
		align-items: center;
		flex: 1;
	}

	.category-icon {
		width: 100rpx;
		height: 100rpx;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 15rpx;
		box-shadow: 0 4rpx 15rpx rgba(0, 0, 0, 0.1);
	}

	.icon-text {
		font-size: 40rpx;
	}

	.category-name {
		font-size: 24rpx;
		color: #333;
		text-align: center;
	}

	/* 排行榜 *//* CSS 样式 */
	.ranking-section {
		 /* 容器整体样式 */
		background-color: white;
		margin: 20rpx 30rpx; /* 居中显示 */
		border-radius: 20rpx;
		padding: 30rpx;
		box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);/* 轻微阴影增加层次感 */
	}

	.section-header {
		display: flex;
		align-items: center;
		margin-bottom: 30rpx;
	}

	.section-title {
		display: flex;
		align-items: center;
		margin-right: 20rpx;
	}

	.red-dot {
		width: 12rpx;
		height: 12rpx;
		background-color: #FF6B6B;
		border-radius: 50%;
		margin-right: 10rpx;
	}

	.section-subtitle {
		font-size: 24rpx;
		color: #666;
		margin-right: auto;
	}

	.more-link {
		font-size: 24rpx;
		color: #FF69B4;
	}

	.ranking-scroll {
		white-space: nowrap;
	}

	.ranking-list {
		display: flex;
		gap: 20rpx;
	}

	.ranking-item {
		position: relative;
		background-color: #FFF5F5;
		border-radius: 15rpx;
		padding: 20rpx;
		min-width: 200rpx;
		box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
	}

	.ranking-badge {
		position: absolute;
		top: -10rpx;
		left: -10rpx;
		width: 40rpx;
		height: 40rpx;
		background: linear-gradient(135deg, #FFD700, #FFA500);
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
		font-weight: bold;
		font-size: 20rpx;
		box-shadow: 0 2rpx 8rpx rgba(255, 215, 0, 0.3);
	}

	.product-image {
		width: 120rpx;
		height: 120rpx;
		margin: 0 auto 15rpx;
		border-radius: 10rpx;
		overflow: hidden;
		background-color: #F0F0F0;
	}

	.product-image image {
		width: 100%;
		height: 100%;
	}

	.product-info {
		text-align: center;
	}

	.hot-tag {
		background-color: #FF69B4;
		color: white;
		font-size: 20rpx;
		padding: 5rpx 15rpx;
		border-radius: 15rpx;
		margin-bottom: 10rpx;
		display: inline-block;
	}

	.product-name {
		font-size: 24rpx;
		color: #333;
		line-height: 1.4;
	}

	/* 新品推荐 */
	.new-products-section {
		background-color: white;
		margin: 20rpx 30rpx;
		border-radius: 20rpx;
		padding: 30rpx;
		box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
	}
         /* 弹性容 */
	.new-products-list {
		 display: flex;         /* 弹性容 */ /* 将该元素定义为弹性容器，其内部的子元素（子节点）会按照弹性盒模型规则排列（默认沿水平方向一行排列）。
		 */
		gap: 20rpx;
	}

	.new-product-item {
		flex: 1;
		background-color: #F8F9FA;
		border-radius: 15rpx;
		padding: 20rpx;
		position: relative;
	}

	.product-image {
		width: 100%;
		height: 150rpx;
		border-radius: 10rpx;
		overflow: hidden;
		background-color: #E9ECEF;
		margin-bottom: 15rpx;
	}

	.product-image image {
		width: 100%;
		height: 100%;
	}

	.product-info {
		margin-bottom:15rpx;
	}

	.product-name {
		font-size: 26rpx;
		color: #333;
		font-weight: bold;
		margin-bottom: 8rpx;
		display: block;
	}

	.product-desc {
		font-size: 22rpx;
		color: #666;
		line-height: 1.4;
		display: block;
	}

	.product-action {
		display: flex;
		flex-direction: column;
		align-items: center;
		position: absolute;
		bottom: 15rpx;
		left: 50%;
		transform: translateX(-50%);
	}

	.action-icon {
		font-size: 25rpx;
		margin-bottom: 5rpx;
	}

	.action-text {
		font-size: 20rpx;
		color: #FF69B4;
	}
	

</style>