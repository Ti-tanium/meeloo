<template>
  <div class="thanks">
      <image mode="widthFix" src="/static/images/posters/thank-world-cup-art.jpg" alt="thanks for you attendance in world cup of art" class="poster"/>
      <div class="button-group">
        <button class="btn" @click="onBack">返回</button>
        <button class="btn" @click="onKnowledge">小知识</button>
      </div>
  </div>
</template>

<script>
export default {
  methods: {
    onBack () {
      wx.navigateBack({
        delta: 1 // 返回的页面数，如果 delta 大于现有页面数，则返回到首页,
      })
    }
  }
}
</script>

<style>
.button-group{
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
.btn{
  background-color: #C83C23;
  color:#fff;
  font-size: 16px;
  border-radius: 2px;
  box-shadow: 2px 2px 5px #333;
  width:200rpx;
  height: 60rpx;
  line-height: 60rpx;
}
.poster{
  width: 100%;
}
</style>