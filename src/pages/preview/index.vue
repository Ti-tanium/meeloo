<template>
  <div class="preview">
      <div class="first">
        <img src="/static/images/world-cup-art.jpg" alt="world cup art" class="world-cup-art">
        <div class="number">NO:{{number}}</div>
        <div class="main-info">

          <image :src="signupInfo.compositionUrl" alt="" class="composition"/>
          <div class="blackboard"></div>

            <div :class='{description_wrap:true, emptyDescription:signupInfo.description==""}'>
              {{signupInfo.description}}
            </div>

        </div>
        <div class="info">姓名：{{signupInfo.name}}</div>
        <div class="info">年龄：{{currentYear-signupInfo.birthday.year}}</div>
        <div class="info">画龄：{{currentYear-signupInfo.startPaintingDay.year}}</div>
        <div class="info">出生：{{signupInfo.birthday.year+"年"+
                                 signupInfo.birthday.month+"月"+
                                 signupInfo.birthday.day+"日"}}</div>
        <div class="info">学画时间：{{signupInfo.startPaintingDay.year+"年"+
                                     signupInfo.startPaintingDay.month+"月"}}</div>
        <div class="info">类别：{{signupInfo.category}}</div>
      </div>
      <div class="second">
        <div class="info">推送单位：{{signupInfo.unit}}</div>
        <div class="info">指导老师：{{signupInfo.advisor}}</div>
      </div>
      <div class="third">
        <div class="info">监护人：{{signupInfo.gardianName}}</div>
        <div class="info">关系：{{signupInfo.gardianRelation}}</div>
        <div class="info">电话：{{signupInfo.phone}}</div>
        <div class="info">邮件：{{signupInfo.email}}</div>
        <div class="info">区域：{{signupInfo.area}}</div>
        <div class="info">地址：{{signupInfo.address}}</div>
        <button class="btn" @click="onConfirm">确认</button>
      </div>
      
  </div>
</template>

<script>
export default {
  data () {
    return {
      number: 2020004,
      signupInfo: {}
    }
  },
  computed: {
    currentYear () {
      return new Date().getFullYear()
    }
  },
  mounted () {
    this.signupInfo = JSON.parse(this.$root.$mp.query.info)
    console.log(this.signupInfo)
  },
  methods: {
    onConfirm () {
      wx.navigateBack({
        delta: 1 // 返回的页面数，如果 delta 大于现有页面数，则返回到首页,
      })
    }
  }
}
</script>

<style>
.preview{
  background-color: #f2f2f2;
}
.world-cup-art{
  width: 360rpx;
  height: 75rpx;
  margin-bottom: 8·px;
}
.number{
  color: #929292;
  font-size: 12px;
}
.composition{
  width: 718rpx;
  height: 508rpx;
}
.info{
  margin: 16px 8px;
  font-size: 14px;
  font-family:Arial, Helvetica, sans-serif;
  color: #040404
}
.main-info{
  display: flex;
  flex-direction: column;
  justify-content: center;
  color: #fff;
  font-size: 8px;
}
.basicInfo-wrap{
  display: flex;
  flex-direction: column;
  position: absolute;
  background-color: rgba(255, 255, 255, 0.55);
  padding: 8px;
  top: 120rpx;
  right: 16rpx;
  color: #000;
}
.basic-info{
  font-size: 10px;
}
.description_wrap{
  background-color: rgba(255, 255, 255, 0.55);
  position: absolute;
  color: #000;
  width: 702rpx;
  max-height: 150rpx;
  padding: 8px;
  font-size: 8px;
  overflow: hidden;
  bottom: 570rpx;
  text-align: left;
  z-index: 1;
}
.emptyDescription{
  display: none;
}

.first{
  margin-bottom: 4rpx;
  padding: 8px;
  background-color: #fff;
}
.second{
  margin-bottom: 4rpx;
  padding: 8px;
  background-color: #fff;
}
.third{
  padding: 8px;
  background-color: #fff;
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
.back{
  position: absolute;
  background-color: rgba(255, 255, 255, 0.55);
  width: 360rpx;
  height: 160rpx;
  top: 430rpx;
  right: 36rpx;
}
</style>