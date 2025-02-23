<template>
  <view class="my">
    <view class="header">
      <view class="user-info">
        <view class='image'>
          <img style="width: 90px;"
            src="https://img12.360buyimg.com/imagetools/jfs/t1/143702/31/16654/116794/5fc6f541Edebf8a57/4138097748889987.png" />
        </view>
        <view class="base-info">
          <view class="name">测试用户</view>
          <view class="tel">18512812208</view>
        </view>
        <view class="setting">
          <IconFont name="setting" color="#eee" size="24"></IconFont>
        </view>
      </view>
    </view>
    <view class="privilege">
      <view class="item">
        <view class="number">0</view>
        <view class="name">月卡</view>
      </view>
      <view class="item">
        <view class="number">0</view>
        <view class="name">精品课</view>
      </view>
      <view class="item">
        <view class="number">0</view>
        <view class="name">小班课</view>
      </view>
      <view class="item">
        <view class="number">0</view>
        <view class="name">私教课</view>
      </view>
    </view>
    <view class="record">
      <view class="overview">
        <view class="total">累计上课</view>
        <IconFont name="arrow-right" color="#64b578" size="14"></IconFont>
      </view>
      <view class="detail">
        <text class="item">0</text><text class="desc">分钟，本周已上课0分钟</text>
      </view>
    </view>

    <view class="service">
      <view class="more">更多服务</view>
      <!-- <nut-divider :style="{ color: '#64b578', borderColor: '#64b578' }"> </nut-divider> -->

      <nut-grid :border="false">
        <nut-grid-item text="我的预约">
          <IconFont name="date" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

        <nut-grid-item text="活动记录">
          <IconFont name="find" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

        <nut-grid-item text="购课记录">
          <IconFont name="cart" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

        <nut-grid-item text="反馈留言">
          <IconFont name="comment" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

        <nut-grid-item text="帮助中心">
          <IconFont name="ask" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

        <nut-grid-item text="分享">
          <IconFont name="share" color="#64b578" size="28"></IconFont>
        </nut-grid-item>

      </nut-grid>
    </view>

  </view>

  <nut-tabbar v-model="active" bottom safe-area-inset-bottom placeholder active-color="#64b578" @tab-switch="tabSwitch">
    <nut-tabbar-item v-for="(item, index) in tabs" :key="index" :tab-title="item.title" :icon="item.icon">
    </nut-tabbar-item>
  </nut-tabbar>
</template>

<script setup>
import { h, ref, onMounted } from 'vue'
import Taro from '@tarojs/taro'
import { IconFont } from '@nutui/icons-vue-taro'
import { Home, My, Footprint, Clock, Dongdong } from '@nutui/icons-vue-taro'
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
const active = ref(3)

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
.my {

  .header {
    height: 520px;
    background: linear-gradient(to right, #64b578, #1de9b6);
    display: flex;

    .user-info {
      padding-top: 100px;
      display: flex;
      align-items: center;
      padding-left: 100px;
      flex-grow: 1;
      height: 200px;

      .base-info {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        flex-grow: 1;
        margin-left: 20px;

        .name {
          font-size: 40px;
          font-weight: bold;
          color: #fff;
        }

        .tel {
          font-size: 32px;
          color: #fff;
        }
      }

      .setting {
        margin-right: 60px;
      }

    }
  }

  .privilege {
    height: 200px;
    background-color: #fff;
    margin: 16px;
    border-radius: 8px;
    display: flex;
    transform: translateY(-50%);

    .item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      flex-grow: 1;

      .number {
        font-size: 40px;
        color: #64b578;
      }

      .name {
        font-size: 28px;
        color: #999;
      }
    }
  }

  .record {
    background-color: #fff;
    margin: 16px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    margin-top: -100px;

    .overview {
      display: flex;
      align-items: center;
      padding: 24px 24px 24px 32px;

      .total {
        font-size: 30px;
        font-weight: bold;
        margin-right: 10px;

      }
    }

    .detail {
      display: flex;
      align-items: baseline;
      padding: 0 24px 24px 32px;

      .item {
        font-size: 48px;
        font-weight: bold;
        color: #64b578;
        margin-right: 10px;
      }

      .desc {
        font-size: 28px;
        color: #999;
      }
    }
  }

  .service {
    background-color: #fff;
    margin: 16px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    padding: 24px 24px 24px 32px;

    .more {
      font-size: 30px;
      font-weight: bold;
      margin-bottom: 20px;
    }
  }

}
</style>
