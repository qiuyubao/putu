<template>
    <view class="search-page">
        <!-- 搜索栏 -->
        <view class="search-header">
            <view class="search-input-wrapper">
                <input 
                    class="search-input" 
                    type="text" 
                    placeholder="搜索商品" 
                    v-model="searchKeyword"
                    @confirm="searchProducts"
                    focus
                />
                <view class="search-btn" @click="searchProducts">
                    <text class="search-icon">🔍</text>
                </view>
            </view>
            <view class="cancel-btn" @click="goBack">
                <text>取消</text>
            </view>
        </view>

        <!-- 搜索历史 -->
        <view class="search-history" v-if="!searchKeyword && searchHistory.length > 0">
            <view class="history-header">
                <text class="history-title">搜索历史</text>
                <view class="clear-btn" @click="clearHistory">
                    <text class="clear-icon">🗑️</text>
                </view>
            </view>
            <view class="history-tags">
                <view 
                    class="history-tag" 
                    v-for="(keyword, index) in searchHistory" 
                    :key="index"
                    @click="selectHistory(keyword)"
                >
                    <text>{{ keyword }}</text>
                </view>
            </view>
        </view>

        <!-- 热门搜索 -->
        <view class="hot-search" v-if="!searchKeyword">
            <view class="hot-header">
                <text class="hot-title">热门搜索</text>
            </view>
            <view class="hot-tags">
                <view 
                    class="hot-tag" 
                    v-for="(keyword, index) in hotKeywords" 
                    :key="index"
                    @click="selectHotKeyword(keyword)"
                >
                    <text>{{ keyword }}</text>
                </view>
            </view>
        </view>

        <!-- 搜索结果 -->
        <view class="search-results" v-if="searchKeyword">
            <view class="results-header">
                <text class="results-count">找到 {{ searchResults.length }} 个相关商品</text>
                <view class="sort-btn" @click="showSortOptions">
                    <text>排序</text>
                    <text class="sort-icon">▼</text>
                </view>
            </view>
            
            <view class="product-list">
                <view 
                    class="product-item" 
                    v-for="(product, index) in searchResults" 
                    :key="index"
                    @click="goToProduct(product)"
                >
                    <view class="product-image">
                        <image :src="product.image" mode="aspectFill"></image>
                    </view>
                    <view class="product-info">
                        <text class="product-name">{{ product.name }}</text>
                        <text class="product-desc">{{ product.description }}</text>
                        <view class="product-bottom">
                            <text class="product-price">¥{{ product.price }}</text>
                            <view class="product-tags">
                                <text class="tag" v-for="tag in product.tags" :key="tag">{{ tag }}</text>
                            </view>
                        </view>
                    </view>
                </view>
            </view>
        </view>

        <!-- 排序选项弹窗 -->
        <view class="sort-modal" v-if="showSort" @click="hideSortOptions">
            <view class="sort-content" @click.stop>
                <view class="sort-title">排序方式</view>
                <view class="sort-options">
                    <view 
                        class="sort-option" 
                        v-for="(option, index) in sortOptions" 
                        :key="index"
                        @click="selectSort(option)"
                    >
                        <text class="option-text">{{ option.name }}</text>
                        <text class="option-check" v-if="currentSort === option.value">✓</text>
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
            searchKeyword: '',
            searchHistory: ['避孕套', '润滑液', '情趣用品', '安全套'],
            hotKeywords: ['杜蕾斯', '冈本', '杰士邦', '倍力乐', '超薄', '持久', '情趣', '润滑'],
            searchResults: [],
            showSort: false,
            currentSort: 'default',
            sortOptions: [
                { name: '综合排序', value: 'default' },
                { name: '价格从低到高', value: 'price_asc' },
                { name: '价格从高到低', value: 'price_desc' },
                { name: '销量排序', value: 'sales' },
                { name: '新品优先', value: 'new' }
            ]
        }
    },
    methods: {
        searchProducts() {
            if (!this.searchKeyword.trim()) {
                uni.showToast({
                    title: '请输入搜索关键词',
                    icon: 'none'
                })
                return
            }
            
            // 添加到搜索历史
            this.addToHistory(this.searchKeyword)
            
            // 模拟搜索结果
            this.searchResults = [
                {
                    id: 1,
                    name: '杜蕾斯超薄避孕套',
                    description: '12只装 超薄体验',
                    price: 29.9,
                    image: '/static/images/condom1.jpg',
                    tags: ['热销', '超薄']
                },
                {
                    id: 2,
                    name: '冈本003超薄',
                    description: '10只装 日本进口',
                    price: 39.9,
                    image: '/static/images/condom2.jpg',
                    tags: ['进口', '超薄']
                },
                {
                    id: 3,
                    name: '杰士邦持久装',
                    description: '8只装 持久体验',
                    price: 49.9,
                    image: '/static/images/condom3.jpg',
                    tags: ['持久', '热销']
                }
            ]
        },
        selectHistory(keyword) {
            this.searchKeyword = keyword
            this.searchProducts()
        },
        selectHotKeyword(keyword) {
            this.searchKeyword = keyword
            this.searchProducts()
        },
        addToHistory(keyword) {
            if (!this.searchHistory.includes(keyword)) {
                this.searchHistory.unshift(keyword)
                if (this.searchHistory.length > 10) {
                    this.searchHistory.pop()
                }
                // 保存到本地存储
                uni.setStorageSync('searchHistory', this.searchHistory)
            }
        },
        clearHistory() {
            uni.showModal({
                title: '确认清除',
                content: '确定要清除搜索历史吗？',
                success: (res) => {
                    if (res.confirm) {
                        this.searchHistory = []
                        uni.removeStorageSync('searchHistory')
                    }
                }
            })
        },
        showSortOptions() {
            this.showSort = true
        },
        hideSortOptions() {
            this.showSort = false
        },
        selectSort(option) {
            this.currentSort = option.value
            this.hideSortOptions()
            // 这里可以根据排序方式重新排序结果
            this.sortResults()
        },
        sortResults() {
            // 根据选择的排序方式排序结果
            switch (this.currentSort) {
                case 'price_asc':
                    this.searchResults.sort((a, b) => a.price - b.price)
                    break
                case 'price_desc':
                    this.searchResults.sort((a, b) => b.price - a.price)
                    break
                case 'sales':
                    // 模拟按销量排序
                    this.searchResults.sort((a, b) => b.id - a.id)
                    break
                case 'new':
                    // 模拟按新品排序
                    this.searchResults.sort((a, b) => a.id - b.id)
                    break
                default:
                    // 默认排序
                    break
            }
        },
        goToProduct(product) {
            uni.navigateTo({
                url: `/pages/product/product?id=${product.id}`
            })
        },
        goBack() {
            uni.navigateBack()
        }
    },
    onLoad() {
        // 加载搜索历史
        const history = uni.getStorageSync('searchHistory')
        if (history) {
            this.searchHistory = history
        }
    }
}
</script>

<style scoped>
.search-page {
    background-color: #F8F8F8;
    min-height: 100vh;
}

.search-header {
    background-color: white;
    padding: 20rpx 30rpx;
    display: flex;
    align-items: center;
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.search-input-wrapper {
    flex: 1;
    display: flex;
    align-items: center;
    background-color: #F8F8F8;
    border-radius: 50rpx;
    padding: 0 30rpx;
    margin-right: 20rpx;
}

.search-input {
    flex: 1;
    height: 70rpx;
    font-size: 28rpx;
    color: #333;
}

.search-btn {
    padding: 10rpx;
}

.search-icon {
    font-size: 28rpx;
    color: #999;
}

.cancel-btn {
    font-size: 28rpx;
    color: #FF69B4;
}

.search-history, .hot-search {
    background-color: white;
    margin: 20rpx 30rpx;
    border-radius: 20rpx;
    padding: 30rpx;
    box-shadow: 0 4rpx 20rpx rgba(0, 0, 0, 0.08);
}

.history-header, .hot-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30rpx;
}

.history-title, .hot-title {
    font-size: 32rpx;
    font-weight: bold;
    color: #333;
}

.clear-btn {
    padding: 10rpx;
}

.clear-icon {
    font-size: 28rpx;
    color: #999;
}

.history-tags, .hot-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 20rpx;
}

.history-tag, .hot-tag {
    background-color: #F8F8F8;
    color: #666;
    padding: 15rpx 30rpx;
    border-radius: 50rpx;
    font-size: 24rpx;
    transition: all 0.3s ease;
}

.history-tag:active, .hot-tag:active {
    background-color: #FF69B4;
    color: white;
}

.search-results {
    padding: 20rpx 30rpx;
}

.results-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30rpx;
    padding: 20rpx 0;
}

.results-count {
    font-size: 24rpx;
    color: #666;
}

.sort-btn {
    display: flex;
    align-items: center;
    font-size: 24rpx;
    color: #FF69B4;
}

.sort-icon {
    margin-left: 10rpx;
    font-size: 20rpx;
}

.product-list {
    display: flex;
    flex-direction: column;
    gap: 20rpx;
}

.product-item {
    background-color: white;
    border-radius: 15rpx;
    padding: 20rpx;
    display: flex;
    box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.product-image {
    width: 150rpx;
    height: 150rpx;
    border-radius: 10rpx;
    overflow: hidden;
    margin-right: 20rpx;
    background-color: #F0F0F0;
}

.product-image image {
    width: 100%;
    height: 100%;
}

.product-info {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.product-name {
    font-size: 28rpx;
    color: #333;
    font-weight: bold;
    margin-bottom: 10rpx;
    line-height: 1.4;
}

.product-desc {
    font-size: 24rpx;
    color: #666;
    margin-bottom: 15rpx;
    line-height: 1.4;
}

.product-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
}

.product-price {
    font-size: 32rpx;
    color: #FF69B4;
    font-weight: bold;
}

.product-tags {
    display: flex;
    gap: 10rpx;
}

.tag {
    background-color: #FF69B4;
    color: white;
    font-size: 20rpx;
    padding: 5rpx 12rpx;
    border-radius: 15rpx;
}

.sort-modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: flex-end;
    z-index: 1000;
}

.sort-content {
    background-color: white;
    width: 100%;
    border-radius: 20rpx 20rpx 0 0;
    padding: 40rpx 30rpx;
}

.sort-title {
    font-size: 32rpx;
    font-weight: bold;
    color: #333;
    text-align: center;
    margin-bottom: 40rpx;
}

.sort-options {
    display: flex;
    flex-direction: column;
}

.sort-option {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30rpx 0;
    border-bottom: 1rpx solid #F0F0F0;
}

.sort-option:last-child {
    border-bottom: none;
}

.option-text {
    font-size: 28rpx;
    color: #333;
}

.option-check {
    font-size: 28rpx;
    color: #FF69B4;
    font-weight: bold;
}
</style>

