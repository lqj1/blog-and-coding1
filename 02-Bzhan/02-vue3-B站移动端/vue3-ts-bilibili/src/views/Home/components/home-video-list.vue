<template>
  <div class="list">
    <!-- 单个视频 -->
    <AppVideoItem v-for="item in list" :key="item.id" :video="item" />
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import AppVideoItem from '@/components/app-video-item.vue';

interface IVideoItem {
  id: number,
  imgSrc: string,
  desc: string,
  playCount: string,
  commentCount: string,
  videoSrc: string
}
const list = ref<IVideoItem[]>([])
axios({
  method: 'get',
  url: '/videosList'
}).then(res=> {
  console.log('视频数据：', res.data.result);
  list.value = res.data.result
})
</script>
<style lang="less">
.list {
  display: flex;
  flex-wrap: wrap;
  padding: 0 1vw;
}
</style>