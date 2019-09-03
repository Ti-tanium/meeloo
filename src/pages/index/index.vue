<template>
  <div class='welcome'>
    <img src='../../../static/images/MEELOO.png' alt='meeloo' class='logo' />
  </div>
</template>

<script>
export default {
  onShow () {
    console.info('Show welcome page.')
    setTimeout(function () {
      console.info('Switching.')
      wx.switchTab({ url: '/pages/home/main' })
    }, 1000)
  }
}
</script>

<style scoped>
.welcome{
  background-color: #7BD4E6;
  background-size: 100% 100%;
  height: 100%;
  display: flex;
  justify-content: center;
}
.logo{
  margin-top: 150rpx;
  height: 44rpx;
  width: 260rpx;
}
</style>
