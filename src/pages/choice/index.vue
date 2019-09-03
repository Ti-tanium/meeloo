<template>
  <div class="choice">
      <img src="/static/images/living-skill.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "living-skill" == target}' 
          id="living-skill">
      <img src="/static/images/charity.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "charity" == target}' 
          id="charity">
      <img src="/static/images/habit.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "habit" == target}' 
          id="habit">
      <img src="/static/images/knowledge.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "knowledge" == target}' 
          id="knowledge">
      <img src="/static/images/oral-english.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "oral-english" == target}' 
          id="oral-english">
      <img src="/static/images/physical.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,active: "physical" == target}' 
          id="physical">
      <img src="/static/images/aesthetic.jpg" 
          @click="onClickBtn" 
          :class='{imgbtn:true,aes_active: "aesthetic" == target,aes_inactive:target!="aesthetic"}'           
          id="aesthetic">
         
      <img src="/static/images/cluster.jpg" alt="cluter" class="cluster">
      <div class="btn-wrap">
        <button class="btn-large" @click="onConfirm">确认</button>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      active: false,
      target: ''
    }
  },
  methods: {
    onClickBtn (e) {
      this.target = e.currentTarget.id
      console.log(this.target)
    },
    onConfirm (e) {
      wx.navigateTo({ url: '/pages/contest-signup/main' })
    }
  }
}
</script>

<style>
.choice{

}
.cluster{
  margin: 300rpx 16rpx;
  width: 100%;
  height: 600rpx;;
}
.imgbtn{
  position:fixed;
  width: 100rpx;
  height: 100rpx;
}
.active{
  filter: saturate(700%);
}
#living-skill{
  bottom: 250rpx;
  right: 100rpx;
}
#charity{
  left: 45%;
  top: 200rpx;
}
#knowledge{
  left: 60rpx;
  bottom: 200rpx;
}
#habit{
  left: 200rpx;
  bottom: 150rpx;
}
#physical{
  right: 280rpx;
  bottom: 230rpx;
}
#oral-english{
  right: 100rpx;
  top: 230rpx;
}
#aesthetic{
  top: 100rpx;
  left: 80rpx;
  width: 80rpx;
  height: 90rpx;
}
.aes_active{
  filter: saturate(1.2)
}
.aes_inactive{
  filter: saturate(0.8) brightness(1.15);
  opacity: 0.6;
}
.btn-large{
  background-color: #7BD4E6;
  position: fixed;
  bottom: 16rpx;
  width: 300rpx;
  height: 80rpx;
  font-size: 16px;
  color: #fff;
  border-radius:40rpx;
}
.btn-wrap{
  display: flex;
  justify-content: center;
}

</style>