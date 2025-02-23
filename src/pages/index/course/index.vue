<template>
  <view class="container">
    <nut-navbar title="课程详情" left-show fixed @click-back="onClickBack"></nut-navbar>
    <!-- 课程封面 -->
    <nut-swiper :auto-play="3000" :height="200" pagination-visible="true">
      <nut-swiper-item v-for="(image, index) in course.swiperImages" :key="index">
        <img :src="image" alt="" style="height: 100%; width: 100%; object-fit: cover;" draggable="false" />
      </nut-swiper-item>
    </nut-swiper>

    <view class="course-detail-container">
      <!-- 课程基本信息 -->
      <view class="course-info">
        <view class="title">{{ course.name }}课程的详细介绍</view>
        <view class="description">{{ course.description }}</view>
      </view>
    </view>
  </view>
</template>

<script setup>
import Taro from '@tarojs/taro';
import { ref } from 'vue';
import courses from "../../../data/course.json"

// 获取路由参数中的用户 ID
const index = Taro.getCurrentInstance().router.params.id;

// 根据用户 ID 获取用户数据
const course = courses[index - 1]

// 返回上一页
const onClickBack = () => {
  console.log('[Navbar]: on click back');
  Taro.navigateBack();
};
</script>

<style scoped>
.container {
  height: 100%;
}

/* 容器样式 */
.course-detail-container {
  padding: 24px;
}

/* 课程封面样式 */
.course-cover {
  width: 100%;
  height: 100%;
}

/* 课程基本信息样式 */
.course-info {
  background-color: #fff;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 32px;
  font-weight: bold;
  color: #333;
  margin-bottom: 16px;
}

.price {
  font-size: 28px;
  color: #ff5722;
  margin-bottom: 16px;
}

.description {
  font-size: 24px;
  color: #666;
  line-height: 1.6;
}

/* 讲师介绍样式 */
.instructor-section {
  margin-top: 24px;
}

.instructor-info {
  display: flex;
  align-items: center;
  padding: 16px;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.instructor-avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin-right: 16px;
}

.instructor-details .name {
  font-size: 28px;
  font-weight: bold;
  color: #333;
  margin-bottom: 8px;
}

.instructor-details .bio {
  font-size: 24px;
  color: #666;
}

/* 课程大纲样式 */
.syllabus-section {
  margin-top: 24px;
}

.syllabus-list {
  padding: 16px;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.syllabus-item {
  font-size: 24px;
  color: #333;
  margin-bottom: 12px;
}
</style>
