<template>
  <div class="video-info">
    <!-- {{videoInfo}} -->
    <div class="title">{{videoInfo.videoTitle}}</div>
    <div class="author-info">
      <div class="author">
        <img :src="videoInfo.authorIconSrc" alt="" class="author-avatar">
        <span class="author-name">{{videoInfo.author}}</span>
      </div>
      <span>{{videoInfo.playCount}}观看</span>
      <span>
        <i class="iconfont dianzan"></i>
        <span>{{videoInfo.likeCount}}</span>
      </span>
      <span>
        <i class="iconfont icon_fav"></i>
        <span>{{videoInfo.favCount}}</span>
      </span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, PropType } from "vue";
import { IVideoInfo } from "../types";
defineProps({
  videoInfo: {
    type: Object as PropType<IVideoInfo>,
    required: true
  }
})
</script>
<style lang="less" scoped>
.video-info {
  padding: 3vw 2vw;
  border-bottom: 1px solid #ddd;
  .title {
    font-size: 4vw;
    line-height: 6vw;
    margin: 3vw 0;
  }
  .author-info {
    display: flex;
    align-items: center;
    font-size: 3vw;
    color: #999;
    .author {
      flex: 1;
      .author-avatar {
        width: 5vw;
        height: 5vw;
        object-fit: cover;
        border-radius: 50%;
        overflow: hidden;
        margin: 0 1vw;
        background: url(~@/assets/images/loading.png) no-repeat center #e7e7e7;
      }
      .author-name {
        color: #212121;
      }
    }
    > span {
      margin: 0 2vw;
    }
    .iconfont {
      font-size: 5vw;
      color: #757575;
      margin-right: 2vw;
    }
  }
}
</style>