<template>
  <view class="container">
    <text class="title">欢迎使用 uni-app</text>
    <button @click="increment">增加</button>
    <text>计数: {{ count }}</text>
  </view>
</template>

<script>
export default {
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    }
  }
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
.title {
  font-size: 24px;
  margin-bottom: 20px;
}
</style>