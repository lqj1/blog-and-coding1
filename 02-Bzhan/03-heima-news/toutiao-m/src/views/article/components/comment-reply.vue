<template>
  <div class="comment-reply">
    <!-- 头部信息 -->
    <van-nav-bar :title="`${comment.reply_count}条回复`">
      <van-icon slot="left" name="cross" @click="$emit('close')"></van-icon>
    </van-nav-bar>
    <!-- /头部信息 -->
    <!-- 当前评论项 -->
    <comment-item
      :comment="comment" />
    <!-- /当前评论项 -->
    <!-- 所有评论回复 -->
    <van-cell title="所有回复" />
    <comment-list :source="comment.com_id" type="c" :list="commentList" />
    <!-- /所有评论回复 -->
    <!-- 评论回复底部 -->
    <div class="article-bottom">
      <div class="flex-div">
        <div class="art-bot-wrap">
          <van-button class="comment-btn" type="default" round size="small" @click="isPostShow = true">写评论
          </van-button>
        </div>
        <!-- 发布回复 -->
        <van-popup
          v-model="isPostShow"
          position="bottom"
        >
          <post-comment
            :target="comment.com_id"
            :article-id="articleId"
            @post-success="onPostSuccess"
          />
        </van-popup>
        <!-- /发布回复 -->
      </div>
    </div>
    <!-- /评论回复底部 -->
  </div>
</template>

<script>
import CommentItem from './comment-item.vue'
import CommentList from './comment-list.vue'
import PostComment from './post-comment.vue'
export default {
  name: 'CommentReply',
  components: {
    CommentItem,
    CommentList,
    PostComment
  },
  props: {
    // 查看回复的评论项
    comment: {
      type: Object,
      required: true
    },
    articleId: {
      type: [Number, String, Object],
      required: true
    }
  },
  data () {
    return {
      isPostShow: false,
      commentList: [] // 评论的回复列表
    }
  },
  methods: {
    onPostSuccess (comment) {
      // 将发布成功的评论放到评论列表的顶部
      this.commentList.unshift(comment)
      // 更新评论回复数量
      this.comment.reply_count++
      // 关闭发布回复的弹出层
      this.isPostShow = false
    }
  }
}
</script>

<style lang="less" scoped>
.article-bottom {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-sizing: border-box;
  height: 44px;
  border-top: 1px solid #d8d8d8;
  background-color: #fff;
  .comment-btn {
    width: 200px;
    height: 30px;
    border: 1px solid #eee;
    font-size: 15px;
    line-height: 23px;
    color: #a7a7a7;
  }
}
</style>
