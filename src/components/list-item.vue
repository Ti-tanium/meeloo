<template>
  <a :href="item.url">
    <div class="list-item">
      <img :src="item.logo" alt="logo" class="logo">
      <div class="label">{{item.label}}</div>
      <div class="description">{{item.description}}</div>
    </div>
  </a>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>

<style>
.list-item{
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 0.7em;
}
.description{
    font-size: 8px;
    color: #999798
}
.logo{
    height: 80rpx;
    width: 100rpx;
}
</style>