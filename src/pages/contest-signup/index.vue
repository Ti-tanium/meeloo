<template>
  <div class="signup">
      <div class="head">
        <img src="/static/images/contest-poster.jpg" alt="contest-poster" class="poster">
      </div>
      <div class="form">
        <img src="/static/images/flag.jpg" alt="flag" class="flag">
        <van-cell-group>
          <div class="basic">
            <div class="half-field">
              <van-field
                :required='true'
                label="姓名："
                placeholder="请输入姓名"
                :value="signupInfo.name"
                @change="onChangeName"
              />

              <van-field
                label="出生："
                :required='true'
                :readonly='true'
                placeholder="请选择出生日期"
                v-model='birthdayString'
                @click="onChooseBirthday"
              />
              <van-popup
                :show="show"
                position="bottom"
                :overlay="true"
                @close="onClose"
                >
                <van-datetime-picker
                  type="date"
                  :value="currentDate"
                  @cancel="onCancelBirthday"
                  @confirm="onConfirmBirthday"
                  :min-date="minDate"
                  :formatter="formatter"
                />
              </van-popup>
              
              <van-field
                label="学画时间："
                :required='true'
                :readonly='true'
                placeholder="选择开始学画时间"
                v-model="startPaintingDayString"
                @click="onChooseStartPaintingDay"
                />
              <van-popup
                :show="showPaintingDayPicker"
                position="bottom"
                :overlay="true"
                @close="onClose"
                >
                <van-datetime-picker
                  v-model="currentDate"
                  type="year-month"
                  :min-date="minDate"
                  :formatter="formatter"
                  @confirm="onConfirmStartPaintingDay"
                />
              </van-popup>
            </div>
            <div class="avatar">
              <img :src="signupInfo.photoURL" alt="" class="photo" @click="uploadPhoto">
              <div class="upload-wrap" @click="uploadPhoto">
                <img src="/static/images/icon/camera.png" alt="camera" class="icon">
                <span>点击上传照片</span>
              </div>
            </div>
          </div>

          <div class="gardian">
            <div class="bifield">
              <van-field
                label="监护人:"
                placeholder="姓名"
                :required='true'
                :value="signupInfo.gardianName"
                @change="onChangeGardianName"
                label-width="70px"
                />
            </div>
            <div class="bifield">
              <picker @change="onPickRelationChange" :value="pickerIndex" name="relation" :range="relationColumns">
                <van-field label="关系:" 
                           v-model="signupInfo.gardianRelation" 
                           placeholder="关系" 
                           :required="true"
                           :disabled="true"/>
              </picker>
            </div>
          </div>

          <van-field
            label="电话："
            :required='true'
            :value="signupInfo.phone"
            @change="onChangePhone"
            placeholder="请输入监护人电话"
            type="number"
            />
          <van-field
            label="邮箱："
            :required='true'
            placeholder="请输入监护人电子邮箱"
            :value="signupInfo.email"
            @change="onChangeEmail"
            />
          <van-field
            label="区域："
            :required='true'
            placeholder="请输入常住省、市、区"
            :value="signupInfo.area"
            @change="onChangeArea"
            />
          <van-field
            label="地址："
            :required='true'
            placeholder="请输入常住地址，精确到小区"
            :value="signupInfo.address"
            @change="onChangeAddress"
            />
          <van-field label="推送单位：" 
                     :value="signupInfo.unit"
                     :required='true'
                     @change="onChangeUnit"
                     placeholder="请输入推送单位"/>
          <van-field label="指导老师：" 
                     :value="signupInfo.advisor" 
                     @change="onChangeAdvisor"
                     :required='true'
                     placeholder="请输入指导老师姓名"/>

          <van-field label="作品名称：" 
                     :value="signupInfo.compositionName" 
                     :required='true'
                     @change="onChangeCompositionName"
                     placeholder="请输入作品名称"/>
          
          <picker @change="onPickCategoryChange" 
                  :value="categoryPickerIndex" 
                  name="category" 
                  :range="categoryColumns">
            <van-field label="类别" :required='true'
                       placeholder="请选择画作类别" 
                       :value="signupInfo.category" 
                       :readonly="true"/>
          </picker>

          <div class="composition-section">
            <span class="prompt">作品提交</span>
            <image mode="aspectFit" :src="signupInfo.compositionUrl" alt="composition" class="composition" @click="uploadComposition"/>
            <div class="upload-wrap" @click="uploadComposition">
              <img src="/static/images/icon/camera.png" alt="camera" class="icon">
              <span>点击上传作品</span>
            </div>

            <span class="prompt">作品描述</span>
            <textarea name="compositionDescription" id="" cols="30" rows="10" 
                      v-model="signupInfo.description"
                      class="textarea-description"
                      placeholder="请输入对作品的描述，200字以内"></textarea>
            
            <div class="button-group">
              <button class="btn" @click="onSubmit">提交</button>
              <button class="btn" @click="onPreview">预览</button>
            </div>

          </div>


          
        </van-cell-group>
      </div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      show: false,
      showPaintingDayPicker: false,
      signupInfo: {
        name: '',
        birthday: {
          year: '',
          month: '',
          day: ''
        },
        startPaintingDay: {
          year: '',
          month: ''
        },
        photoURL: '',
        gardianName: '',
        gardianRelation: '',
        phone: '',
        email: '',
        area: '',
        unit: '',
        advisor: '',
        address: '',
        compositionName: '',
        category: '',
        compositionUrl: '',
        description: ''
      },
      currentDate: new Date().getTime(),
      minDate: new Date(0).getTime(),
      relationColumns: ['父子', '母子'],
      categoryColumns: ['环境保护', '梦想', '友谊'],
      categoryPickerIndex: 0,
      pickerIndex: 0
    }
  },
  computed: {
    birthdayString () {
      return this.signupInfo.birthday.day ? this.signupInfo.birthday.year + '年' +
      this.signupInfo.birthday.month + '月' + this.signupInfo.birthday.day + '日' : ''
    },
    startPaintingDayString () {
      return this.signupInfo.startPaintingDay.month ? this.signupInfo.startPaintingDay.year + '年' +
      this.signupInfo.startPaintingDay.month + '月' : ''
    }
  },
  methods: {
    onClose () {
      this.show = false
      this.showPaintingDayPicker = false
      this.showRelation = false
    },
    onChooseBirthday () {
      this.show = true
    },
    onConfirmBirthday (value) {
      let date = new Date(value.mp.detail)
      this.signupInfo.birthday.year = date.getFullYear()
      this.signupInfo.birthday.month = date.getMonth() + 1
      this.signupInfo.birthday.day = date.getDate()
      this.show = false
    },
    onCancelBirthday () {
      this.show = false
    },
    onChooseStartPaintingDay () {
      this.showPaintingDayPicker = true
    },
    onConfirmStartPaintingDay (e) {
      let date = new Date(e.mp.detail)
      this.signupInfo.startPaintingDay.year = date.getFullYear()
      this.signupInfo.startPaintingDay.month = date.getMonth() + 1
      this.showPaintingDayPicker = false
    },
    uploadPhoto () {
      wx.chooseImage({
        count: '1', // 最多可以选择的图片张数,
        success: res => {
          this.signupInfo.photoURL = res.tempFilePaths[0]
        }, // 返回图片的本地文件路径列表 tempFilePaths,
        fail: () => {},
        complete: () => {}
      })
    },
    onPickRelationChange (e) {
      this.pickerIndex = e.target.value
      this.signupInfo.gardianRelation = this.relationColumns[this.pickerIndex]
    },
    onPickCategoryChange (e) {
      this.categoryPickerIndex = e.target.value
      this.signupInfo.category = this.categoryColumns[this.categoryPickerIndex]
    },
    onSubmit (e) {
      wx.navigateTo({ url: '/pages/thanks/main' })
    },
    onPreview (e) {
      console.log(this.signupInfo)
      wx.navigateTo({ url: '/pages/preview/main?info=' + JSON.stringify(this.signupInfo) })
    },
    uploadComposition () {
      wx.chooseImage({
        count: '1', // 最多可以选择的图片张数,
        success: res => {
          this.signupInfo.compositionUrl = res.tempFilePaths[0]
        }, // 返回图片的本地文件路径列表 tempFilePaths,
        fail: () => {},
        complete: () => {}
      })
    },

    onChangeCompositionName (e) {
      this.signupInfo.compositionName = e.mp.detail
    },
    onChangeAdvisor (e) {
      this.signupInfo.advisor = e.mp.detail
    },
    onChangePhone (e) {
      this.signupInfo.phone = e.mp.detail
    },
    onChangeEmail (e) {
      this.signupInfo.email = e.mp.detail
    },
    onChangeArea (e) {
      this.signupInfo.area = e.mp.detail
    },
    onChangeAddress (e) {
      this.signupInfo.address = e.mp.detail
    },
    onChangeUnit (e) {
      this.signupInfo.unit = e.mp.detail
    },
    onChangeName (e) {
      this.signupInfo.name = e.mp.detail
    },
    onChangeGardianName (e) {
      this.signupInfo.gardianName = e.mp.detail
    }

  }
}
</script>

<style>
.basic{
  display: flex;
  flex: row;
}
.photo{
  background-color: #f2f2f2;  
  width: 200rpx;
  height: 250rpx;
  margin: 0 0 4px 0;
}
.avatar{
  width: 35%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.poster{
  width: 100%;
}
.flag{
  width: 120rpx;
  height: 50rpx;
  margin-top: 16rpx;
}
.half-field{
  width: 65%;
}
.bifield{
  width: 45%;
}
.icon{
  width: 16px;
  height: 16px;
}
.upload-wrap{
  display: flex;
  flex-direction: row;
  align-items: center;
  font-size: 10px;
}
.gardian{
  display: flex;
  flex-direction: row;
}

.composition-section{
  margin: 30rpx;
}
.composition{
  background-color: #f2f2f2;
  width: 100%;
  height: 300rpx;
  margin: 8px 0;
}
.prompt{
  color: #0e0e0e;
  font-size: 14px;
  margin-top: 8px;
}
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
.textarea-description{
  margin: 8px 0;
}
</style>