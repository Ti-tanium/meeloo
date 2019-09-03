<template>
  <div class="home">
    <div class="head">
      <img src="/static/images/icon/scan.png" alt="scan" class="icon" @click="onScan"/>
      <van-search placeholder="请输入关键词" background="#fff" class="search"/>
      <img src="/static/images/icon/chat.png" alt="chat" class="icon" />
    </div>
    <van-tabs :active="active" @change="onChange"  color="#AE6F22">
      <van-tab title="推荐">
        <img src="/static/images/banner.jpg" alt="banner" class="banner">
        <div class="nav">
          <ListItem v-for="item in list_items" :key="item.id" :item="item" @click="onTapItem"></ListItem>
        </div>
      </van-tab>
      <van-tab title="此刻">此刻</van-tab>
      <van-tab title="体验">体验</van-tab>
      <van-tab title="资讯">资讯</van-tab>
    </van-tabs>
    <div class="qrcode-wrap">
      <div class="qrcode">
        <img src="/static/images/icon/qrcode.png" alt="qrcode" class="qrcode-icon"/>
      </div>
    </div>
  </div>
</template>

<script>
import ListItem from '../../components/list-item'
export default {
  components: {
    ListItem
  },
  data () {
    return {
      active: 0,
      list_items: [
        {
          id: 0,
          logo: '/static/images/icon/holiday-improve.jpg',
          label: '假期提升',
          description: '专项性主题技能提升',
          url: ''
        },
        {
          id: 1,
          logo: '/static/images/icon/world-contest.jpg',
          label: '环球赛场',
          description: '更大舞台的挑战',
          url: ''
        },
        {
          id: 2,
          logo: '/static/images/icon/world-bank.jpg',
          label: '世界银行',
          description: '未来的美好生活',
          url: ''
        },
        {
          id: 3,
          logo: '/static/images/icon/toolbox.jpg',
          label: '工具箱',
          description: '路路联合更多优质资源',
          url: '/pages/choice/main'
        }
      ]
    }
  },
  methods: {
    onChange () {},
    onTapItem (item) {
      console.log(item)
    },
    onScan () {
      wx.scanCode({
        onlyFromCamera: false, // 是否只能从相机扫码，不允许从相册选择图片,
        success: res => {}
      })
    },
    onShareAppMessage () {
      return {
        title: '麋鹿国际',
        path: '/pages/home/main',
        success: res => {},
        fail: () => {},
        complete: () => {}
      }
    }
  }
}
</script>

<style scoped>
.icon {
  height: 32rpx;
  width: 32rpx;
}
.search {
  width: 100%;
}
.head {
  padding: 0 16rpx;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.banner{
  width: 100%;
  height: 300rpx;
}
.nav{
  display: flex;
  align-content: flex-start;
  justify-content: space-around;
}
.qrcode{
  position: fixed;
  bottom: 4rpx;
  z-index: 9999;
  width: 90rpx;
  height:90rpx;
  border-radius: 40rpx;
  background-color: #7BD4E6;
  box-shadow: 1px 1px 5px #333;
  display: flex;
  justify-content: center;
  align-items: center;
}
.qrcode-icon{
  width: 50rpx;
  height: 50rpx;
}
.qrcode-wrap{
  display: flex;
  justify-content: center;
}
</style>