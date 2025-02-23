<template>
  <view class="container">
    <nut-navbar title="公告详情" left-show fixed @click-back="onClickBack"></nut-navbar>

    <view class="announcement-container">
      <!-- 公告标题 -->
      <view class="announcement-title">{{ announcement.title }}</view>

      <!-- 发布时间 -->
      <view class="announcement-time">{{ announcement.time }}</view>

      <!-- 公告内容 -->
      <view class="announcement-content">
        <rich-text :nodes="announcement.content"></rich-text>
      </view>
    </view>
  </view>
</template>

<script setup>
import Taro from '@tarojs/taro';
import { ref, onMounted } from 'vue';

// 模拟公告数据
const announcement = ref({
  title: '浅愈.普拉提美学运动工作室开业公告',
  time: '2025-02-24 10:00',
  content: `
    <p>尊敬的顾客朋友们：</p>
    <p style="text-indent: 2em">我们非常高兴地宣布，浅愈.普拉提美学运动工作室即将隆重开业！经过精心筹备和努力，我们为您带来了一个全新的运动体验。</p>
    <p style="text-indent: 2em">在开业期间，我们为您准备了丰厚的优惠活动和精美的礼品，期待您的光临！</p>
    <p style="text-indent: 2em">我们的团队将竭诚为您提供优质的服务，让您感受到运动的乐趣和健康的生活方式。</p>
    <p style="text-indent: 2em">感谢您一直以来对我们的支持和厚爱，我们将继续努力，为您带来更多的惊喜和便利。</p>
    <p style="text-indent: 2em">敬请期待！</p>
    <p style="display:flex;justify-content:flex-end">浅愈.普拉提美学运动工作室</p>
  `
});

// 返回上一页
const onClickBack = () => {
  console.log('[Navbar]: on click back');
  Taro.navigateTo({
    url: '/pages/index/index'
  })
};

// 页面加载时的逻辑（如果有需要从接口获取公告详情）
onMounted(() => {
  // 示例：从后端获取公告详情
  // fetchAnnouncementDetail();
});
</script>

<style scoped>
.container {
  height: 100%;
}

/* 容器样式 */
.announcement-container {
  padding: 24px;
}

/* 标题样式 */
.announcement-title {
  font-size: 36px;
  font-weight: bold;
  color: #333;
  margin-bottom: 16px;
}

/* 时间样式 */
.announcement-time {
  font-size: 24px;
  color: #666;
  margin-bottom: 24px;
}

/* 内容样式 */
.announcement-content {
  font-size: 28px;
  color: #333;
  line-height: 1.6;
  background-color: #fff;
  padding: 24px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
