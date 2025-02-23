<template>
  <view class="container">

    <!-- 导航栏 -->
    <nut-navbar title="关于我们" left-show fixed @click-back="onClick"></nut-navbar>

    <!-- Banner 图 -->
    <nut-swiper class="swiper" :auto-play="3000" :height="200" pagination-visible="true">
      <nut-swiper-item v-for="(image, index) in swiperImages" :key="index">
        <img :src="image" alt="" style="height: 100%; width: 100%; object-fit: cover;" draggable="false" />
      </nut-swiper-item>
    </nut-swiper>
    <view class="about-us">
      <!-- 工作室简介 -->
      <view class="section introduction">
        <view class="section-title">关于浅愈.普拉提 .SPA</view>
        <view class="section-content">
          <p style="text-indent: 2em;">欢迎来到【浅愈.普拉提 .SPA】——一个专注于身心灵平衡与健康的温馨空间。</p>
          <p style="text-indent: 2em;">2025年成立于成都，一个专注都市人群身心健康和身材管理的疗愈运动品牌，由两位对生活充满热情、的95后女生所创立。</p>
        </view>
      </view>

      <!-- 我们的理念 -->
      <view class="section philosophy">
        <view class="section-title">我们的理念</view>
        <view class="philosophy-list">
          <view v-for="(item, index) in philosophy" :key="index" class="philosophy-item">
            <IconFont :name="item.icon" size="24" color="#67C23A" />
            <text class="philosophy-text">{{ item.text }}</text>
          </view>
        </view>
      </view>

      <!-- 团队成员 -->
      <view class="section team">
        <view class="section-title">我们的团队</view>
        <view class="team-list">
          <view v-for="(member, index) in team" :key="index" class="team-member" @click="showDetail(member.id)">
            <image :src="member.avatar" class="member-avatar" />
            <view class="member-info">
              <text class="member-name">{{ member.name }}</text>
              <text class="member-role">{{ member.role }}</text>
              <p class="member-description">{{ member.desc }}</p>
            </view>
          </view>
        </view>
      </view>

      <!-- 成就展示 -->
      <!-- <view class="section achievements">
        <view class="section-title">我们的成就</view>
        <view class="achievements-grid">
          <view v-for="(achievement, index) in achievements" :key="index" class="achievement-item">
            <IconFont :name="achievement.icon" size="32" color="#67C23A" />
            <text class="achievement-text">{{ achievement.text }}</text>
          </view>
        </view>
      </view> -->

      <!-- 联系方式 -->
      <view class="section contact">
        <view class="section-title">联系我们</view>
        <view class="contact-info">
          <text>地址：{{ contact.address }}</text>
          <text>电话：{{ contact.phone }}</text>
        </view>
        <nut-button type="primary" color="#64b578" block @click="openMap">导航到我们</nut-button>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';
import Taro from '@tarojs/taro';
import { IconFont } from '@nutui/icons-vue-taro';
import team from "../../../data/teacher.json";

// 工作室理念数据
const philosophy = ref([
  { icon: 'heart', text: '健康' },
  { icon: 'retweet', text: '平衡' },
  { icon: 'home', text: '专注' },
]);

const swiperImages = ref([
  'https://free4.yunpng.top/2025/02/23/67ba0ec316ef7.jpg',
  'https://free4.yunpng.top/2025/02/23/67ba0ec451146.jpg',
  'https://free4.yunpng.top/2025/02/23/67ba0ede0ee17.jpg'
])

// 成就数据
const achievements = ref([
  { icon: 'trophy', text: '2020年荣获年度最佳瑜伽工作室称号' },
  { icon: 'expand', text: '2023年开设新教室，扩大服务范围' },
]);

// 联系方式数据
const contact = ref({
  address: '成都市郫都区犀浦华都路龙湖映辰4栋1单元401',
  phone: '010-12345678',
});

// 打开地图导航
const openMap = () => {
  Taro.openLocation({
    latitude: 39.9042,
    longitude: 116.4074,
    name: '瑜伽工作室',
    address: contact.value.address,
  });
};

const onClick = () => {
  console.log('[Navbar]: on click back')
  Taro.navigateTo({
    url: '/pages/index/index'
  })
}

const showDetail = (index) => {
  console.log('点击了第' + index + '个教练')
  Taro.navigateTo({ url: `/pages/index/coach/detail/index?id=${index}` })
}
</script>

<style scoped>
.container {
  height: 100%;
}

.about-us {
  padding: 20px;
  margin: 16px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;

  background-color: #fff;

}

.banner {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-bottom: 20px;
}

.section {
  margin-bottom: 12px;
}

.section-title {
  font-size: 28px;
  font-weight: bold;
  color: #333;
  margin-bottom: 10px;
}

.introduction .section-content {
  font-size: 24px;
  line-height: 1.6;
  color: #666;
}

.philosophy-list {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.philosophy-item {
  text-align: center;
}

.philosophy-text {
  display: block;
  margin-top: 10px;
  font-size: 20px;
  color: #333;
}

.team-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 20px;
}

.team-member {
  display: flex;
  align-items: center;
  background-color: #fff;
  width: 100%;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.member-avatar {
  width: 5.6rem;
  height: 3rem;
  border-radius: 50%;
  margin-right: 10px;
}

.member-name {
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

.member-role {
  font-size: 24px;
  color: #666;
  margin-left: 12px;
}

.member-description {
  font-size: 24px;
  color: #999;
}

.achievements-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.achievement-item {
  text-align: center;
}

.achievement-text {
  display: block;
  margin-top: 10px;
  font-size: 20px;
  color: #333;
}

.contact-info {
  margin-bottom: 20px;
  font-size: 24px;
  color: #666;
}

.contact-info text {
  display: block;
  margin-bottom: 5px;
}
</style>
