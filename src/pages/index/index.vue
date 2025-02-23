<template>
  <view>
    <nut-swiper :auto-play="3000" :height="300" pagination-visible="true">
      <nut-swiper-item v-for="(item, index) in swipers" :key="index" @click="handSwiperClick(index)">
        <img :src="item" alt="" style="height: 100%; width: 100%; object-fit: cover;" draggable="false" />
      </nut-swiper-item>
    </nut-swiper>

    <view class="container">
      <view class="desc">
        <view class="brand">
          <view class='image'>
            <img style="width: 100px;" :src="logo" />
          </view>
          <view class="shop">
            <view class="name">浅愈.普拉提美学运动工作室</view>
            <view class="sub-title">提升女性的健康与美感</view>
          </view>
          <view @click="toShop">
            <IconFont name="shop" color="#64b578" size="24"></IconFont>
          </view>
        </view>
        <nut-divider :style="{ color: '#64b578', padding: '5px 16px', margin: '30px 0 0 0' }"> </nut-divider>
        <view class="contact">
          <!--地址-->
          <view class="address">
            <IconFont name="location2" color="#64b578" @click="openMap"></IconFont>
            <view class="address-text">成都市郫都区犀浦华都路龙湖映辰4栋1单元401</view>
          </view>
          <!--电话-->
          <view class="phone">
            <IconFont name="service" color="#64b578" @click="callPhone"></IconFont>
            <view class="phone-text">010-88888888</view>
          </view>

        </view>
      </view>

      <view class="notice" @click="showNotice">
        <nut-noticebar :text="text" scrollable background="#64b578" color="#fff">
          <template #left-icon>
            <img
              src="https://img13.360buyimg.com/imagetools/jfs/t1/72082/2/3006/1197/5d130c8dE1c71bcd6/e48a3b60804c9775.png"
              style="width: 20px; height: 20px" />
          </template>
          <template #right-icon>
            <IconFont name="rect-right"></IconFont>
          </template>
          <!-- <template #left-icon>
            <IconFont name="message" class="nut-icon-am-breathe nut-icon-am-infinite"></IconFont>
          </template> -->
        </nut-noticebar>
      </view>

      <view class="course">
        <view class="title">课程介绍</view>
        <nut-grid :border="false">
          <nut-grid-item v-for="item in course" :key="item.id" @click="showCourseDetail(item.id)">
            <nut-avatar size="large" shape="square" bg-color="transparent">
              <img :src="item.image" style="border-radius: 40%;" />
            </nut-avatar>
            <view class="name">{{ item.name }}</view>
          </nut-grid-item>
        </nut-grid>
      </view>

      <view class="team">
        <view class="title">
          <view class="name">团队介绍</view>
          <view class="show-more" @click="showMore">
            <text>更多</text>
            <IconFont name="rect-right" color="#64b578"></IconFont>
          </view>
        </view>
        <view class="detail">
          <nut-space :gutter="16">
            <view v-for="item in teacher" :key="item.id" class="desc" @click="showDetail(item.id)">
              <nut-avatar size="large">
                <img :src="item.avatar" />
              </nut-avatar>
              <view class="leader">{{ item.name }}</view>
            </view>
          </nut-space>
        </view>

      </view>

      <!-- <view class="recommend">
        <view class="place">
          <nut-swiper :auto-play="3000" :height="210" :loop="true" pagination-visible="true">
            <nut-swiper-item v-for="(item, index) in list" :key="index">
              <img :src="item" alt="" style="height: 100%; width: 100%" draggable="false" />
            </nut-swiper-item>
          </nut-swiper>
        </view>
        <view class="my-data">
          <nut-empty image="empty" description="今日课程"></nut-empty>
        </view>

      </view> -->

      <view class="about">
        <!-- 标题区域 -->
        <view class="title">
          <view class="name">工作室介绍</view>
          <view class="show-more" @click="showStudioMore">
            <text>更多</text>
            <IconFont name="rect-right" color="#64b578"></IconFont>
          </view>
        </view>

        <!-- 内容区域 -->
        <view class="detail">
          <view class="about-us">
            <!-- 工作室简介 -->
            <view class="section">
              <view class="section-content">
                <view class="content-item">
                  【浅愈.普拉提 .SPA】2025年成立于成都，一个专注都市人群身心健康和身材管理的疗愈运动品牌，由两位对生活充满热情的95后女生所创立。
                </view>
                <view class="content-item">
                  当下是一个快速发展的时代，人们没有过多时间关照自我需求，时感身心疲惫。于是在大环境下，很多人也有了身体或身心的问题。在当下的环境，慢下来、回归自然成了一种向往。
                </view>
                <view class="content-item">
                  带着对生活的追求与自我精神世界的探索，终于决定打破常规，做真正有意义的事——从身心灵三个纬度打造女性的健康与美。于是就有了成都首家结合冥想颂SPA与普拉提的疗愈空间。
                </view>
                <view class="content-item">
                  <text class="meaning-of-life">人生的意义并非仅仅追求物质上的满足，更要追求精神上的富足。</text>
                </view>
                <view class="content-item">
                  如今，【浅愈 普拉提 SPA】疗愈品牌正以它独特的方式，为更多人带去身心愉悦的体验。而那两位女性创业者，也正在用他们的热爱，等待下一个寻求答案的人，带着新的故事和梦，来到这片人间寂静处，找回本我心。
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>


    <!-- <nut-tabbar v-model="active" bottom safe-area-inset-bottom placeholder active-color="#64b578"
      @tab-switch="tabSwitch">
      <nut-tabbar-item v-for="(item, index) in tabs" :key="index" :tab-title="item.title" :icon="item.icon">
      </nut-tabbar-item>
    </nut-tabbar> -->
  </view>
</template>
<script setup>
import { Clock, Footprint, Home, IconFont, My } from '@nutui/icons-vue-taro'
import Taro from '@tarojs/taro'
import { h, onMounted, ref } from 'vue'
import course from "../../data/course.json"
import teacher from "../../data/teacher.json"
import logo from "../../assest/logo.jpg"

const swipers = ref()

const text = ref(
  '浅愈.普拉提美学运动工作室即将隆重开业啦！！！'
)

onMounted(() => {
  setTimeout(() => {
    swipers.value = [
      'https://free4.yunpng.top/2025/02/23/67ba0802cbb1a.jpg',
      'https://free4.yunpng.top/2025/02/23/67ba08030d6af.jpg',
      'https://free4.yunpng.top/2025/02/23/67bb281b634c9.jpg',
      'https://free4.yunpng.top/2025/02/23/67ba0980d2025.jpg',
      'https://free4.yunpng.top/2025/02/23/67ba0980caaac.jpg',
      'https://free4.yunpng.top/2025/02/23/67ba09fa403ac.jpg',
    ]
  }, 0)
})

// 添加轮播图点击事件
const handSwiperClick = (index) => {
  console.log('点击了第' + index + '张轮播图')
}

const showMore = () => {
  console.log('点击了更多')
  Taro.navigateTo({ url: '/pages/index/coach/list/index' })
}

const showStudioMore = () => {
  console.log('点击了更多')
  Taro.navigateTo({ url: '/pages/index/about/index' })
}

const showDetail = (index) => {
  console.log('点击了第' + index + '个教练')
  Taro.navigateTo({ url: `/pages/index/coach/detail/index?id=${index}` })
}

const showNotice = () => {
  Taro.navigateTo({ url: '/pages/index/notice/index' })
}

const showCourseDetail = (index) => {
  console.log('点击了第' + index + '个课程')
  Taro.navigateTo({ url: `/pages/index/course/index?id=${index}` })
}


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
const active = ref(0)

const tabSwitch = (item, index) => {
  console.log(item, index)
  active.value = index
  const path = tabs[index].url;
  if (path) {
    Taro.navigateTo({ url: path });
  }
}

// 打开地图导航
const openMap = () => {
  // 定义目标位置的经纬度
  const latitude = 39.908754; // 纬度 (例如：北京天安门)
  const longitude = 116.39743; // 经度 (例如：北京天安门)

  // 调用 openLocation 打开地图
  Taro.openLocation({
    latitude, // 目标纬度
    longitude, // 目标经度
    name: '天安门广场', // 地点名称 (可选)
    address: '北京市东城区长安街', // 地址详情 (可选)
    scale: 18, // 缩放比例 (可选)
    success: function () {
      console.log('成功调起地图');
    },
    fail: function (err) {
      console.error('调起地图失败', err);
    }
  });
}

const callPhone = () => {
  Taro.makePhoneCall({
    phoneNumber: '13800138000' //仅为示例，并非真实的电话号码
  })
}


const toShop = () => {
  console.log('点击了去门店')
  Taro.navigateTo({ url: '/pages/index/about/index' })
}

const studios = ref([
  'https://via.placeholder.com/300',
  'https://via.placeholder.com/300',
  'https://via.placeholder.com/300'
])

</script>

<style lang="scss" scoped>
.container {

  .desc {
    background-color: #fff;
    margin: 8px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;

    .brand {
      position: relative;
      height: 100px;
      display: flex;
      align-items: center;
      justify-content: space-around;

      .image {
        position: absolute;
        top: 50%;
        left: 15%;
        transform: translate(-50%, -50%);
        border-radius: 50%;
        background-color: rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .shop {
        margin-left: 5rem;

        display: flex;
        flex-direction: column;
        justify-content: center;

        .name {
          font-size: 0.85rem;
          font-weight: bold;
        }

        .sub-title {
          font-size: 0.6rem;
          color: #999;
          margin-top: 0.2rem;
        }
      }
    }

    .contact {
      display: flex;
      flex-direction: column;
      margin-bottom: 0.5rem;

      .address {
        display: flex;
        align-items: center;
        padding-left: 0.4rem;

        .address-text {
          margin-left: 0.5rem;
          font-size: 0.75rem;
        }
      }

      .phone {
        display: flex;
        align-items: center;
        padding-left: 0.4rem;

        .phone-text {
          margin-left: 0.5rem;
          font-size: 0.75rem;
        }
      }
    }
  }

  .course {
    margin: 16px;
    border-radius: 8px;

    .title {
      background: #fff;
      font-size: 0.8rem;
      padding: 0.5rem 0.5rem 0 0.5rem;
    }

    .name {
      font-size: 0.6rem;
      font-weight: 600;
      padding: 6px;
    }
  }

  .notice {
    margin: 16px;
    border-radius: 8px;
  }

  .team {
    background-color: #fff;
    margin: 16px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;

    .title {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem 0.5rem 0 0.5rem;

      .name {
        font-size: 0.8rem;
      }

      .show-more {
        font-size: 0.6rem;
        color: #999;
        display: flex;
        align-items: center;
      }
    }

    .detail {
      display: flex;
      justify-content: space-between;
      padding: 0.3rem;
      //超出左边可以滑动
      overflow-x: scroll;

      //隐藏滚动条
      &::-webkit-scrollbar {
        display: none;
      }

      .desc {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 8px 16px 8px 16px;

        .leader {
          font-size: 0.6rem;
          font-weight: 600;
          padding: 0.5rem;
        }
      }


    }
  }

  .recommend {
    margin: 16px;
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    // margin-bottom: 2.8rem;

    .place {
      width: 50%;
      border-radius: 10px;
    }

    .my-data {
      width: 50%;
      background-color: #fff;
      border-radius: 10px;
      margin-left: 20px;


    }
  }

  .about {
    background-color: #fff;
    margin: 16px;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    // margin-bottom: 2.8rem;

    .title {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem 0.5rem 0 0.5rem;

      .name {
        font-size: 0.8rem;
      }

      .show-more {
        font-size: 0.6rem;
        color: #999;
        display: flex;
        align-items: center;
      }
    }

    .detail {
      background-color: #fff;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

      .section {
        margin-bottom: 20px;

        .section-content {
          font-size: 24px;
          line-height: 1.6;
          color: #666;

          .content-item {
            margin-bottom: 10px;
            text-indent: 2ch;
          }

        }
      }
    }
  }
}
</style>
