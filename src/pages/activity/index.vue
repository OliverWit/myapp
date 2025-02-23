<template>
  <view class="activity">
    <nut-searchbar v-model="keyword" placeholder="搜索活动" clearable
      background="linear-gradient(to right, #64b578, #1de9b6)" input-background="#fff">
      <template #leftin>
        <Search2 style="color: #64b578;" />
      </template>
    </nut-searchbar>
    <view class="activity-list">
      <view class="activity-item">
        <view class="activity-img">
          <image
            src="https://images.unsplash.com/photo-1719937206158-cad5e6775044?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            mode="aspectFill" />
        </view>
        <view class="activity-info">
          <view class="activity-title">2025年国庆秋游活动</view>
          <view class="activity-time">
            <IconFont name="clock" color="#64b578"></IconFont>
            <view class="time">2025-10-01 09:00-15:00</view>
          </view>
          <view class="activity-address">
            <IconFont name="location2" color="#64b578"></IconFont>
            <view class="address">北京市朝阳区</view>
          </view>
          <view class="activity-status">
            <nut-tag color="#64b578"> 未开始 </nut-tag>
          </view>
        </view>
      </view>

      <view class="activity-item">
        <view class="activity-img">
          <image
            src="https://images.unsplash.com/photo-1719937206158-cad5e6775044?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            mode="aspectFill" />
        </view>
        <view class="activity-info">
          <view class="activity-title">2025年元旦春游活动</view>
          <view class="activity-time">
            <IconFont name="clock" color="#64b578"></IconFont>
            <view class="time">2025-01-01 09:00-15:00</view>
          </view>
          <view class="activity-address">
            <IconFont name="location2" color="#64b578"></IconFont>
            <view class="address">北京市朝阳区</view>
          </view>
          <view class="activity-status">
            <nut-tag color="#FA685D"> 已结束 </nut-tag>
          </view>
        </view>
      </view>
    </view>
  </view>
  <nut-divider :style="{ color: '#64b578', padding: '5px 16px' }">没有更多活动啦 </nut-divider>
  <nut-tabbar v-model="active" bottom safe-area-inset-bottom placeholder active-color="#64b578" @tab-switch="tabSwitch">
    <nut-tabbar-item v-for="(item, index) in tabs" :key="index" :tab-title="item.title" :icon="item.icon">
    </nut-tabbar-item>
  </nut-tabbar>
</template>

<script setup>
import { h, ref, onMounted } from 'vue'
import Taro from '@tarojs/taro'
import { IconFont } from '@nutui/icons-vue-taro'
import { Home, My, Footprint, Clock, Search2 } from '@nutui/icons-vue-taro'

const keyword = ref('')

const tabs = [
  {
    title: '首页',
    icon: h(Home),
    url: '/pages/index/index'
  },
  {
    title: '活动',
    icon: h(Footprint),
    url: '/pages/activity/index'
  },
  {
    title: '预约',
    icon: h(Clock),
    url: '/pages/reservation/index'
  },
  {
    title: '我的',
    icon: h(My),
    url: '/pages/my/index'
  }
]
const active = ref(1)

const tabSwitch = (item, index) => {
  console.log(item, index)
  active.value = index
  const path = tabs[index].url;
  if (path) {
    Taro.navigateTo({ url: path });
  }
}
</script>
<style lang="scss" scoped>
.activity {
  padding: 20px;

  .activity-list {
    margin-top: 20px;

    .activity-item {
      display: flex;
      margin-bottom: 20px;
      background-color: #fff;
      border-radius: 16px;
      height: 200px;

      .activity-img {
        width: 240px;
        border-radius: 16px;
        margin-right: 20px;

        image {
          width: 100%;
          height: 100%;
          object-fit: cover;
        }
      }

      .activity-info {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        flex-grow: 1;

        .activity-title {
          font-size: 30px;
          font-weight: bold;
        }

        .activity-time,
        .activity-address,
        .activity-status {
          display: flex;
          align-items: center;
          font-size: 24px;
          color: #999;
          margin-bottom: 5px;

          .time {
            margin-left: 10px;
          }
        }
      }
    }
  }
}
</style>
