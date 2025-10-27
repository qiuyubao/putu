<template>
    <view id="app">
        <!-- 全局组件可以在这里定义 -->
    </view>
</template>

<script>
export default {
    onLaunch: function() {
        console.log('App Launch')
    },
    onShow: function() {
        console.log('App Show')
    },
    onHide: function() {
        console.log('App Hide')
    }
}
</script>

<style>
/* 全局样式 */
page {
    background-color: #F8F8F8;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen', 'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
}

/* 通用样式 */
.container {
    padding: 0 30rpx;
}

.flex {
    display: flex;
}

.flex-center {
    display: flex;
    align-items: center;
    justify-content: center;
}

.flex-between {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.text-center {
    text-align: center;
}

.text-primary {
    color: #FF69B4;
}

.text-white {
    color: #ffffff;
}

.bg-primary {
    background-color: #FF69B4;
}

.bg-white {
    background-color: #ffffff;
}

.border-radius {
    border-radius: 10rpx;
}

.shadow {
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.1);
}

/* 按钮样式 */
.btn {
    padding: 20rpx 40rpx;
    border-radius: 50rpx;
    text-align: center;
    font-size: 28rpx;
    border: none;
    outline: none;
}

.btn-primary {
    background-color: #FF69B4;
    color: #ffffff;
}

.btn-outline {
    background-color: transparent;
    border: 2rpx solid #FF69B4;
    color: #FF69B4;
}

/* 卡片样式 */
.card {
    background-color: #ffffff;
    border-radius: 20rpx;
    padding: 30rpx;
    margin-bottom: 20rpx;
    box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
}

/* 图标样式 */
.icon {
    width: 40rpx;
    height: 40rpx;
}

.icon-large {
    width: 60rpx;
    height: 60rpx;
}

/* 间距 */
.mt-10 { margin-top: 10rpx; }
.mt-20 { margin-top: 20rpx; }
.mt-30 { margin-top: 30rpx; }
.mb-10 { margin-bottom: 10rpx; }
.mb-20 { margin-bottom: 20rpx; }
.mb-30 { margin-bottom: 30rpx; }
.ml-10 { margin-left: 10rpx; }
.mr-10 { margin-right: 10rpx; }
.p-10 { padding: 10rpx; }
.p-20 { padding: 20rpx; }
.p-30 { padding: 30rpx; }
</style>
