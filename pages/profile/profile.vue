<template>
    <view class="profile-page">
        <!-- 用户信息头部 -->
        <view class="profile-header">
            <view class="user-info">
                <view class="avatar">
                    <image src="/static/images/avatar.png" mode="aspectFill"></image>
                </view>
                <view class="user-details">
                    <text class="username">用户昵称</text>
                    <text class="user-level">VIP会员</text>
                </view>
            </view>
            <view class="settings-btn" @click="goToSettings">
                <text class="settings-icon">⚙️</text>
            </view>
        </view>

        <!-- 订单状态 -->
        <view class="order-status">
            <view class="status-item" @click="goToOrders('all')">
                <text class="status-count">0</text>
                <text class="status-label">全部订单</text>
            </view>
            <view class="status-item" @click="goToOrders('pending')">
                <text class="status-count">0</text>
                <text class="status-label">待付款</text>
            </view>
            <view class="status-item" @click="goToOrders('shipping')">
                <text class="status-count">0</text>
                <text class="status-label">待发货</text>
            </view>
            <view class="status-item" @click="goToOrders('delivered')">
                <text class="status-count">0</text>
                <text class="status-label">待收货</text>
            </view>
            <view class="status-item" @click="goToOrders('review')">
                <text class="status-count">0</text>
                <text class="status-label">待评价</text>
            </view>
        </view>

        <!-- 功能菜单 -->
        <view class="menu-section">
            <view class="menu-item" @click="goToAddress">
                <view class="menu-icon">📍</view>
                <text class="menu-text">收货地址</text>
                <text class="menu-arrow">></text>
            </view>
            <view class="menu-item" @click="goToCoupons">
                <view class="menu-icon">🎫</view>
                <text class="menu-text">优惠券</text>
                <text class="menu-arrow">></text>
            </view>
            <view class="menu-item" @click="goToFavorites">
                <view class="menu-icon">❤️</view>
                <text class="menu-text">我的收藏</text>
                <text class="menu-arrow">></text>
            </view>
            <view class="menu-item" @click="goToHistory">
                <view class="menu-icon">🕒</view>
                <text class="menu-text">浏览历史</text>
                <text class="menu-arrow">></text>
            </view>
        </view>

        <!-- 服务菜单 -->
        <view class="menu-section">
            <view class="menu-item" @click="goToCustomerService">
                <view class="menu-icon">💬</view>
                <text class="menu-text">客服中心</text>
                <text class="menu-arrow">></text>
            </view>
            <view class="menu-item" @click="goToPrivacy">
                <view class="menu-icon">🔒</view>
                <text class="menu-text">隐私保护</text>
                <text class="menu-arrow">></text>
            </view>
            <view class="menu-item" @click="goToAbout">
                <view class="menu-icon">ℹ️</view>
                <text class="menu-text">关于我们</text>
                <text class="menu-arrow">></text>
            </view>
        </view>

        <!-- 退出登录 -->
        <view class="logout-section">
            <view class="logout-btn" @click="logout">
                <text>退出登录</text>
            </view>
        </view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            userInfo: {
                nickname: '用户昵称',
                level: 'VIP会员',
                avatar: '/static/images/avatar.png'
            }
        }
    },
    methods: {
        goToSettings() {
            uni.navigateTo({
                url: '/pages/settings/settings'
            })
        },
        goToOrders(status) {
            uni.navigateTo({
                url: `/pages/orders/orders?status=${status}`
            })
        },
        goToAddress() {
            uni.navigateTo({
                url: '/pages/address/address'
            })
        },
        goToCoupons() {
            uni.navigateTo({
                url: '/pages/coupons/coupons'
            })
        },
        goToFavorites() {
            uni.navigateTo({
                url: '/pages/favorites/favorites'
            })
        },
        goToHistory() {
            uni.navigateTo({
                url: '/pages/history/history'
            })
        },
        goToCustomerService() {
            uni.navigateTo({
                url: '/pages/service/service'
            })
        },
        goToPrivacy() {
            uni.navigateTo({
                url: '/pages/privacy/privacy'
            })
        },
        goToAbout() {
            uni.navigateTo({
                url: '/pages/about/about'
            })
        },
        logout() {
            uni.showModal({
                title: '确认退出',
                content: '确定要退出登录吗？',
                success: (res) => {
                    if (res.confirm) {
                        // 清除用户数据
                        uni.removeStorageSync('userInfo')
                        uni.removeStorageSync('token')
                        uni.showToast({
                            title: '已退出登录',
                            icon: 'success'
                        })
                    }
                }
            })
        }
    }
}
</script>

<style scoped>
.profile-page {
    background-color: #F8F8F8;
    min-height: 100vh;
}

.profile-header {
    background: linear-gradient(135deg, #FF69B4, #FF1493);
    padding: 40rpx 30rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
}

.user-info {
    display: flex;
    align-items: center;
}

.avatar {
    width: 120rpx;
    height: 120rpx;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 30rpx;
    border: 4rpx solid rgba(255, 255, 255, 0.3);
}

.avatar image {
    width: 100%;
    height: 100%;
}

.user-details {
    display: flex;
    flex-direction: column;
}

.username {
    font-size: 36rpx;
    font-weight: bold;
    margin-bottom: 10rpx;
}

.user-level {
    font-size: 24rpx;
    opacity: 0.8;
    background-color: rgba(255, 255, 255, 0.2);
    padding: 8rpx 20rpx;
    border-radius: 20rpx;
    text-align: center;
}

.settings-btn {
    padding: 20rpx;
}

.settings-icon {
    font-size: 40rpx;
}

.order-status {
    background-color: white;
    margin: 20rpx 30rpx;
    border-radius: 20rpx;
    padding: 40rpx 0;
    display: flex;
    justify-content: space-around;
    box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
}

.status-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: 1;
}

.status-count {
    font-size: 48rpx;
    font-weight: bold;
    color: #FF69B4;
    margin-bottom: 10rpx;
}

.status-label {
    font-size: 24rpx;
    color: #666;
}

.menu-section {
    background-color: white;
    margin: 20rpx 30rpx;
    border-radius: 20rpx;
    overflow: hidden;
    box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
}

.menu-item {
    display: flex;
    align-items: center;
    padding: 30rpx;
    border-bottom: 1rpx solid #F0F0F0;
    transition: background-color 0.3s ease;
}

.menu-item:last-child {
    border-bottom: none;
}

.menu-item:active {
    background-color: #F8F8F8;
}

.menu-icon {
    font-size: 40rpx;
    margin-right: 30rpx;
    width: 50rpx;
    text-align: center;
}

.menu-text {
    flex: 1;
    font-size: 28rpx;
    color: #333;
}

.menu-arrow {
    font-size: 24rpx;
    color: #999;
}

.logout-section {
    padding: 40rpx 30rpx;
}

.logout-btn {
    background-color: #FF6B6B;
    color: white;
    padding: 25rpx;
    border-radius: 15rpx;
    text-align: center;
    font-size: 28rpx;
    font-weight: bold;
    box-shadow: 0 4rpx 15rpx rgba(255, 107, 107, 0.3);
}
</style>

