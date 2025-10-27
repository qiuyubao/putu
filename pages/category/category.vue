<template>
    <view class="category-page">
        <view class="category-header">
            <text class="category-title">{{ categoryName }}</text>
        </view>
        
        <view class="product-grid">
            <view class="product-item" v-for="(product, index) in products" :key="index" @click="goToProduct(product)">
                <view class="product-image">
                    <image :src="product.image" mode="aspectFill"></image>
                </view>
                <view class="product-info">
                    <text class="product-name">{{ product.name }}</text>
                    <text class="product-price">¥{{ product.price }}</text>
                    <view class="product-tags">
                        <text class="tag" v-for="tag in product.tags" :key="tag">{{ tag }}</text>
                    </view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            categoryName: '商品分类',
            products: [
                {
                    id: 1,
                    name: '杜蕾斯超薄避孕套',
                    price: 29.9,
                    image: '/static/images/condom1.jpg',
                    tags: ['热销', '超薄']
                },
                {
                    id: 2,
                    name: '冈本003超薄',
                    price: 39.9,
                    image: '/static/images/condom2.jpg',
                    tags: ['进口', '超薄']
                },
                {
                    id: 3,
                    name: '杰士邦持久装',
                    price: 49.9,
                    image: '/static/images/condom3.jpg',
                    tags: ['持久', '热销']
                },
                {
                    id: 4,
                    name: '倍力乐情趣装',
                    price: 35.9,
                    image: '/static/images/condom4.jpg',
                    tags: ['情趣', '新品']
                }
            ]
        }
    },
    onLoad(options) {
        if (options.type) {
            this.categoryName = options.type
            this.loadProducts(options.type)
        }
    },
    methods: {
        loadProducts(type) {
            // 根据分类加载不同商品
            const productMap = {
                '男性用品': [
                    { id: 1, name: '男性用品1', price: 99.9, image: '/static/images/male1.jpg', tags: ['热销'] },
                    { id: 2, name: '男性用品2', price: 199.9, image: '/static/images/male2.jpg', tags: ['新品'] }
                ],
                '女性用品': [
                    { id: 3, name: '女性用品1', price: 149.9, image: '/static/images/female1.jpg', tags: ['热销'] },
                    { id: 4, name: '女性用品2', price: 299.9, image: '/static/images/female2.jpg', tags: ['进口'] }
                ],
                '飞机杯': [
                    { id: 5, name: '飞机杯1', price: 89.9, image: '/static/images/cup1.jpg', tags: ['热销'] },
                    { id: 6, name: '飞机杯2', price: 159.9, image: '/static/images/cup2.jpg', tags: ['新品'] }
                ],
                '润滑液': [
                    { id: 7, name: '润滑液1', price: 39.9, image: '/static/images/lube1.jpg', tags: ['热销'] },
                    { id: 8, name: '润滑液2', price: 59.9, image: '/static/images/lube2.jpg', tags: ['进口'] }
                ],
                '避孕套': [
                    { id: 9, name: '避孕套1', price: 29.9, image: '/static/images/condom1.jpg', tags: ['热销'] },
                    { id: 10, name: '避孕套2', price: 49.9, image: '/static/images/condom2.jpg', tags: ['超薄'] }
                ]
            }
            this.products = productMap[type] || this.products
        },
        goToProduct(product) {
            uni.navigateTo({
                url: `/pages/product/product?id=${product.id}`
            })
        }
    }
}
</script>

<style scoped>
.category-page {
    background-color: #F8F8F8;
    min-height: 100vh;
}

.category-header {
    background-color: white;
    padding: 30rpx;
    text-align: center;
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.category-title {
    font-size: 36rpx;
    font-weight: bold;
    color: #333;
}

.product-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20rpx;
    padding: 30rpx;
}

.product-item {
    background-color: white;
    border-radius: 15rpx;
    overflow: hidden;
    box-shadow: 0 4rpx 15rpx rgba(0, 0, 0, 0.08);
    transition: transform 0.3s ease;
}

.product-item:active {
    transform: scale(0.98);
}

.product-image {
    width: 100%;
    height: 200rpx;
    background-color: #F0F0F0;
}

.product-image image {
    width: 100%;
    height: 100%;
}

.product-info {
    padding: 20rpx;
}

.product-name {
    font-size: 28rpx;
    color: #333;
    font-weight: bold;
    margin-bottom: 10rpx;
    display: block;
    line-height: 1.4;
}

.product-price {
    font-size: 32rpx;
    color: #FF69B4;
    font-weight: bold;
    margin-bottom: 15rpx;
    display: block;
}

.product-tags {
    display: flex;
    gap: 10rpx;
    flex-wrap: wrap;
}

.tag {
    background-color: #FF69B4;
    color: white;
    font-size: 20rpx;
    padding: 5rpx 12rpx;
    border-radius: 15rpx;
}
</style>

