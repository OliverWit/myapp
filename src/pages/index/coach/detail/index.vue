<template>
  <nut-navbar title="教练详情" left-show fixed @click-back="onClick"></nut-navbar>
  <view class="detail-page">
    <!-- 顶部 Swiper -->
    <nut-swiper class="swiper" :auto-play="3000" :height="200" pagination-visible="true">
      <nut-swiper-item v-for="(image, index) in user.swiperImages" :key="index">
        <img :src="image" alt="" style="height: 100%; width: 100%; object-fit: cover;" draggable="false" />
      </nut-swiper-item>
    </nut-swiper>

    <!-- 中间介绍 -->
    <view class="detail-content">
      <view class="title">{{ user.name }}老师的详细介绍</view>
      <view class="description"><text style="font-weight:bold;font-size:0.75rem">从业经验:</text>{{ user.detail.exp }}
      </view>
      <view class="description"><text style="font-weight:bold;font-size:0.75rem">课程特色:</text>{{ user.detail.feature }}
      </view>
      <view class="description"><text style="font-weight:bold;font-size:0.75rem">教学风格:</text>{{ user.detail.style }}
      </view>
    </view>
  </view>
</template>

<script setup>
import Taro from '@tarojs/taro';
import users from "../../../../data/teacher.json";

// 获取路由参数中的用户 ID
const userId = Taro.getCurrentInstance().router.params.id;

// 根据用户 ID 获取用户数据
const user = users[userId - 1]

const onClick = () => {
  Taro.navigateBack();
}
</script>

<style scoped>
.swiper-image {
  width: 100%;
  height: 100%;
}

/* 详情内容样式 */
.detail-content {
  margin: 16px;
  background-color: #fff;
  border-radius: 12px;
  padding: 24px;
}

.title {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 10px;
}

.description {
  font-size: 24px;
  color: #666;
  line-height: 1.5;
  padding: 10px
}
</style>
