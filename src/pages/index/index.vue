<template>
  <view class="index">
    <nut-button type="primary" @click="onClick">按钮</nut-button>
    <nut-toast v-model:visible="show" msg="你成功了" />
  </view>
</template>

<script setup>
import { ref } from 'vue';
import Taro from '@tarojs/taro'
// import Taro from '@tarojs/taro';


const show = ref(false)
const onClick = () => {
  Taro.navigateTo({
    url: '/pages/player/index'
  })
}
</script>
