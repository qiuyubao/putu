<template>
    <view class="cart-page">
        <view class="cart-header">
            <text class="cart-title">购物车</text>
            <text class="cart-count">({{ cartItems.length }})</text>
        </view>

        <view class="cart-content" v-if="cartItems.length > 0">
            <view class="cart-item" v-for="(item, index) in cartItems" :key="index">
                <view class="item-checkbox" @click="toggleSelect(index)">
                    <view class="checkbox" :class="{ checked: item.selected }">
                        <text class="checkmark" v-if="item.selected">✓</text>
                    </view>
                </view>
                <view class="item-image">
                    <image :src="item.image" mode="aspectFill"></image>
                </view>
                <view class="item-info">
                    <text class="item-name">{{ item.name }}</text>
                    <text class="item-spec">{{ item.spec }}</text>
                    <view class="item-bottom">
                        <text class="item-price">¥{{ item.price }}</text>
                        <view class="quantity-control">
                            <view class="quantity-btn" @click="decreaseQuantity(index)">-</view>
                            <text class="quantity">{{ item.quantity }}</text>
                            <view class="quantity-btn" @click="increaseQuantity(index)">+</view>
                        </view>
                    </view>
                </view>
                <view class="item-delete" @click="removeItem(index)">
                    <text class="delete-icon">🗑️</text>
                </view>
            </view>
        </view>

        <view class="empty-cart" v-else>
            <view class="empty-icon">🛒</view>
            <text class="empty-text">购物车空空如也</text>
            <text class="empty-desc">快去选购心仪的商品吧</text>
            <view class="go-shopping-btn" @click="goShopping">
                <text>去购物</text>
            </view>
        </view>

        <view class="cart-footer" v-if="cartItems.length > 0">
            <view class="footer-left">
                <view class="select-all" @click="toggleSelectAll">
                    <view class="checkbox" :class="{ checked: allSelected }">
                        <text class="checkmark" v-if="allSelected">✓</text>
                    </view>
                    <text class="select-all-text">全选</text>
                </view>
            </view>
            <view class="footer-right">
                <view class="total-info">
                    <text class="total-label">合计：</text>
                    <text class="total-price">¥{{ totalPrice }}</text>
                </view>
                <view class="checkout-btn" @click="checkout">
                    <text>结算({{ selectedCount }})</text>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            cartItems: [
                {
                    id: 1,
                    name: '杜蕾斯超薄避孕套',
                    spec: '12只装',
                    price: 49.9,
                    quantity: 2,
                    image: '/static/images/condom1.jpg',
                    selected: true
                },
                {
                    id: 2,
                    name: '冈本003超薄',
                    spec: '10只装',
                    price: 39.9,
                    quantity: 1,
                    image: '/static/images/condom2.jpg',
                    selected: false
                }
            ]
        }
    },
    computed: {
        allSelected() {
            return this.cartItems.length > 0 && this.cartItems.every(item => item.selected)
        },
        selectedCount() {
            return this.cartItems.filter(item => item.selected).length
        },
        totalPrice() {
            return this.cartItems
                .filter(item => item.selected)
                .reduce((total, item) => total + (item.price * item.quantity), 0)
                .toFixed(2)
        }
    },
    methods: {
        toggleSelect(index) {
            this.cartItems[index].selected = !this.cartItems[index].selected
        },
        toggleSelectAll() {
            const shouldSelectAll = !this.allSelected
            this.cartItems.forEach(item => {
                item.selected = shouldSelectAll
            })
        },
        increaseQuantity(index) {
            this.cartItems[index].quantity++
        },
        decreaseQuantity(index) {
            if (this.cartItems[index].quantity > 1) {
                this.cartItems[index].quantity--
            }
        },
        removeItem(index) {
            uni.showModal({
                title: '确认删除',
                content: '确定要删除这个商品吗？',
                success: (res) => {
                    if (res.confirm) {
                        this.cartItems.splice(index, 1)
                    }
                }
            })
        },
        goShopping() {
            uni.switchTab({
                url: '/pages/index/index'
            })
        },
        checkout() {
            if (this.selectedCount === 0) {
                uni.showToast({
                    title: '请选择商品',
                    icon: 'none'
                })
                return
            }
            uni.navigateTo({
                url: '/pages/checkout/checkout'
            })
        }
    }
}
</script>

<style scoped>
.cart-page {
    background-color: #F8F8F8;
    min-height: 100vh;
    padding-bottom: 120rpx;
}

.cart-header {
    background-color: white;
    padding: 30rpx;
    text-align: center;
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.cart-title {
    font-size: 36rpx;
    font-weight: bold;
    color: #333;
}

.cart-count {
    font-size: 24rpx;
    color: #999;
    margin-left: 10rpx;
}

.cart-content {
    padding: 20rpx;
}

.cart-item {
    background-color: white;
    border-radius: 15rpx;
    padding: 20rpx;
    margin-bottom: 20rpx;
    display: flex;
    align-items: center;
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.item-checkbox {
    margin-right: 20rpx;
}

.checkbox {
    width: 40rpx;
    height: 40rpx;
    border: 2rpx solid #ddd;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
}

.checkbox.checked {
    background-color: #FF69B4;
    border-color: #FF69B4;
}

.checkmark {
    color: white;
    font-size: 24rpx;
    font-weight: bold;
}

.item-image {
    width: 120rpx;
    height: 120rpx;
    border-radius: 10rpx;
    overflow: hidden;
    margin-right: 20rpx;
    background-color: #F0F0F0;
}

.item-image image {
    width: 100%;
    height: 100%;
}

.item-info {
    flex: 1;
}

.item-name {
    font-size: 28rpx;
    color: #333;
    font-weight: bold;
    margin-bottom: 8rpx;
    display: block;
}

.item-spec {
    font-size: 24rpx;
    color: #999;
    margin-bottom: 15rpx;
    display: block;
}

.item-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.item-price {
    font-size: 32rpx;
    color: #FF69B4;
    font-weight: bold;
}

.quantity-control {
    display: flex;
    align-items: center;
    background-color: #F8F8F8;
    border-radius: 20rpx;
    overflow: hidden;
}

.quantity-btn {
    width: 60rpx;
    height: 60rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #E0E0E0;
    font-size: 28rpx;
    color: #666;
    transition: background-color 0.3s ease;
}

.quantity-btn:active {
    background-color: #D0D0D0;
}

.quantity {
    padding: 0 20rpx;
    font-size: 28rpx;
    color: #333;
    min-width: 80rpx;
    text-align: center;
}

.item-delete {
    margin-left: 20rpx;
    padding: 10rpx;
}

.delete-icon {
    font-size: 32rpx;
}

.empty-cart {
    text-align: center;
    padding: 100rpx 30rpx;
}

.empty-icon {
    font-size: 120rpx;
    margin-bottom: 30rpx;
}

.empty-text {
    font-size: 32rpx;
    color: #333;
    font-weight: bold;
    margin-bottom: 15rpx;
    display: block;
}

.empty-desc {
    font-size: 24rpx;
    color: #999;
    margin-bottom: 40rpx;
    display: block;
}

.go-shopping-btn {
    background-color: #FF69B4;
    color: white;
    padding: 20rpx 60rpx;
    border-radius: 50rpx;
    font-size: 28rpx;
    font-weight: bold;
    display: inline-block;
}

.cart-footer {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: white;
    padding: 20rpx 30rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 -2rpx 10rpx rgba(0, 0, 0, 0.1);
}

.footer-left {
    display: flex;
    align-items: center;
}

.select-all {
    display: flex;
    align-items: center;
}

.select-all-text {
    font-size: 28rpx;
    color: #333;
    margin-left: 15rpx;
}

.footer-right {
    display: flex;
    align-items: center;
}

.total-info {
    margin-right: 30rpx;
}

.total-label {
    font-size: 28rpx;
    color: #333;
}

.total-price {
    font-size: 32rpx;
    color: #FF69B4;
    font-weight: bold;
}

.checkout-btn {
    background-color: #FF69B4;
    color: white;
    padding: 20rpx 40rpx;
    border-radius: 50rpx;
    font-size: 28rpx;
    font-weight: bold;
}
</style>

