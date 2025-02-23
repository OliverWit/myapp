<template>
  <view class="reservation">
    <!--显示最近一周的日期-->
    <view class="date-picker">
      <view v-for="(date, index) in dates" :key="index" class="date" :class="{ 'selected': index === selectedIndex }"
        @click="selectDate(index)">
        <view>{{ date.label }}</view>
        <view>{{ date.day }}</view>
      </view>

    </view>


    <nut-tabs v-model="value" type="smile" align="left" size="large" title-gutter="10" auto-height>
      <nut-tab-pane title="精品课" pane-key="1">
        <view class="course">
          <view class="course-time">
            <view class="time-info">
              <IconFont name="clock" color="#64b578"></IconFont>
              <view class="time">18:30-19:30</view>
            </view>

            <view class="people">满6人开课</view>
          </view>
          <view class="course-info">
            <view style="display: flex;align-items: center;">
              <nut-avatar size="large">
                <img
                  src="https://img12.360buyimg.com/imagetools/jfs/t1/196430/38/8105/14329/60c806a4Ed506298a/e6de9fb7b8490f38.png" />
              </nut-avatar>
              <view class="course-desc">
                <view class="course-name">上肢训练</view>
                <view class="teacher-name">
                  <IconFont name="my" color="#64b578"></IconFont>
                  <view>王老师</view>
                </view>
                <view class="course-address">
                  <IconFont name="location2" color="#64b578"></IconFont>
                  <view>北京市朝阳区</view>
                </view>
              </view>
            </view>
            <view class="course-btn">
              <nut-button color="#FA685D" @click="reservate">已结束</nut-button>
            </view>
          </view>
          <view class="participants">
            <nut-avatar-group max-count="3" z-index="left" max-content="..." size="small">
              <nut-avatar size="small"><img
                  src="https://img12.360buyimg.com/imagetools/jfs/t1/143702/31/16654/116794/5fc6f541Edebf8a57/4138097748889987.png" /></nut-avatar>
              <nut-avatar size="small">
                <My />
              </nut-avatar>
              <nut-avatar size="small" color="rgb(245, 106, 0)" bg-color="rgb(253, 227, 207)">小明</nut-avatar>
              <nut-avatar size="small">
                <My />
              </nut-avatar>
            </nut-avatar-group>
          </view>
        </view>
        <view class="course">
          <view class="course-time">
            <view class="time-info">
              <IconFont name="clock" color="#64b578"></IconFont>
              <view class="time">18:30-19:30</view>
            </view>

            <view class="people">满6人开课</view>
          </view>
          <view class="course-info">
            <view style="display: flex;align-items: center;">
              <nut-avatar size="large">
                <img
                  src="https://img12.360buyimg.com/imagetools/jfs/t1/196430/38/8105/14329/60c806a4Ed506298a/e6de9fb7b8490f38.png" />
              </nut-avatar>
              <view class="course-desc">
                <view class="course-name">手臂训练(女子器械)</view>
                <view class="teacher-name">
                  <IconFont name="my" color="#64b578"></IconFont>
                  <view>王老师</view>
                </view>
                <view class="course-address">
                  <IconFont name="location2" color="#64b578"></IconFont>
                  <view>北京市朝阳区</view>
                </view>
              </view>
            </view>
            <view class="course-btn">
              <nut-button color="#64b578" @click="reservate">预约</nut-button>
            </view>
          </view>
          <view class="participants">
            <nut-avatar-group max-count="3" z-index="left" max-content="..." size="small">
              <nut-avatar size="small"><img
                  src="https://img12.360buyimg.com/imagetools/jfs/t1/143702/31/16654/116794/5fc6f541Edebf8a57/4138097748889987.png" /></nut-avatar>
              <nut-avatar size="small">
                <My />
              </nut-avatar>
              <nut-avatar size="small" color="rgb(245, 106, 0)" bg-color="rgb(253, 227, 207)">小明</nut-avatar>
              <nut-avatar size="small">
                <My />
              </nut-avatar>
            </nut-avatar-group>
          </view>
        </view>
      </nut-tab-pane>
      <nut-tab-pane title="私教课" pane-key="2">
        <view class="course">
          Content 2
        </view>
      </nut-tab-pane>
      <nut-tab-pane title="小班课" pane-key="3">
        <view class="course">
          Content 3
        </view>

      </nut-tab-pane>
    </nut-tabs>

    <nut-tabbar v-model="active" bottom safe-area-inset-bottom placeholder active-color="#64b578"
      @tab-switch="tabSwitch">
      <nut-tabbar-item v-for="(item, index) in tabs" :key="index" :tab-title="item.title" :icon="item.icon">
      </nut-tabbar-item>
    </nut-tabbar>
  </view>
</template>

<script setup>
import { h, ref, onMounted } from 'vue'
import Taro from '@tarojs/taro'
import { IconFont } from '@nutui/icons-vue-taro'
import { Home, My, Footprint, Clock } from '@nutui/icons-vue-taro'

const value = ref('1')

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
const active = ref(2)

const tabSwitch = (item, index) => {
  console.log(item, index)
  active.value = index
  const path = tabs[index].url;
  if (path) {
    Taro.navigateTo({ url: path });
  }
}

const generateDates = () => {
  const today = new Date();
  const dates = [];
  for (let i = 0; i < 7; i++) {
    const date = new Date(today);
    date.setDate(today.getDate() + i); // 计算未来第 i 天的日期
    const dayOfWeek = getDayOfWeek(date); // 获取星期几
    const dayOfMonth = date.getDate(); // 获取具体日期
    dates.push({
      label: dayOfWeek,
      day: dayOfMonth,
    });
  }
  return dates;
}
const getDayOfWeek = (date) => {
  const daysOfWeek = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];
  return daysOfWeek[date.getDay()];
}


const dates = ref(generateDates())
const selectedIndex = ref(0)

const selectDate = (index) => {
  selectedIndex.value = index
}

const reservate = () => {
  console.log('预约')
}
</script>
<style lang="scss" scoped>
.reservation {
  padding: 20px;

  .date-picker {
    display: flex;
    margin: 12px 6px;
    justify-content: space-between;

    .date {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 80px;
      height: 100px;
      border-radius: 10px;
      background-color: #fff;
      color: #999999;
      margin-right: 20px;
      transition: background-color 0.3s ease;

      &.selected {
        color: #fff;
        background-color: #64b578;
        /* 绿色 */
      }

      view {
        font-size: 28px;
        margin-bottom: 5px
      }
    }
  }

  .course {
    height: 360px;
    background-color: #fff;
    border-radius: 10px;
    margin-top: 20px;
    display: flex;
    flex-direction: column;

    .course-time {
      display: flex;
      flex: 0 0 auto;
      padding: 16px;
      align-items: center;
      justify-content: space-between;

      .time-info {
        display: flex;
        align-items: center;

        .time {
          display: flex;
          justify-content: flex-start;
          align-items: center;
          font-size: 28px;
          margin-left: 10px;
          color: #999;
        }
      }

      .people {
        font-size: 28px;
        color: #999;
      }
    }

    .course-info {
      padding: 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;

      .course-desc {
        margin-left: 12px;

        .course-name {
          font-size: 30px;
          font-weight: bold;
          margin-bottom: 10px;
        }

        .teacher-name {
          display: flex;
          align-items: center;
          font-size: 24px;
          color: #999;
          margin-bottom: 10px;
        }

        .course-address {
          display: flex;
          align-items: center;
          font-size: 24px;
          color: #999;
        }
      }
    }

    .participants {
      padding: 16px;
      display: flex;
    }
  }
}
</style>
