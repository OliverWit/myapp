<template>
  <view class="container">
    <nut-navbar title="教练列表" left-show fixed @click-back="onClick"></nut-navbar>
    <view class="user-list">
      <nut-cell v-for="user in users" :key="user.id" class="user-item" @click="onUserClick(user)">
        <!-- 左侧头像 -->
        <view class="avatar-container">
          <image :src="user.avatar" class="avatar" mode="aspectFill"></image>
        </view>

        <!-- 右侧内容 -->
        <view class="content">
          <view class="username">{{ user.name }}</view>
          <view class="description">{{ user.role }}</view>
        </view>
      </nut-cell>
    </view>

    <nut-divider :style="{ color: '#64b578', padding: '5px 16px' }">没有更多教练啦 </nut-divider>
  </view>
</template>

<script setup>
import Taro from '@tarojs/taro';
import users from "../../../../data/teacher.json";


const onClick = () => {
  console.log('[Navbar]: on click back')
  Taro.navigateTo({
    url: '/pages/index/index'
  })
}

const onUserClick = (user) => {
  console.log('[User]: on click', user)
  Taro.navigateTo({
    url: `/pages/index/coach/detail/index?id=${user.id}`
  })
}
</script>

<style scoped>
.container {
  height: 100%;
}
/* 列表容器 */
.user-list {
  padding: 16px;
}

/* 列表项 */
.user-item {
  display: flex;
  align-items: center;
  padding: 12px;
  margin-bottom: 8px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  /* 添加阴影效果 */
  transition: transform 0.2s ease-in-out;
  /* 添加悬停动画 */
}

.user-item:hover {
  transform: translateY(-4px);
  /* 悬停时轻微上移 */
}

/* 头像容器 */
.avatar-container {
  margin-right: 16px;
}

/* 头像样式 */
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  border: 2px solid #eaeaea;
  /* 添加边框，增强视觉效果 */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  /* 添加阴影 */
}

/* 内容区域 */
.content {
  flex: 1;
}

/* 用户名样式 */
.username {
  font-size: 32px;
  font-weight: bold;
  color: #333;
  margin-bottom: 12px;
}

/* 描述样式 */
.description {
  font-size: 24px;
  color: #666;
  line-height: 1.4;
}
</style>
