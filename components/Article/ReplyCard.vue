<template>
  <div class="cmt reply">
    <div class="head">
      <span style="color: #37acc9;">{{comment.author.company.name}}</span>
      <span>·</span>
      <span>{{comment.author.nickname}}</span>
    </div>
    <div class="body">
      <div class="content">{{comment.content}}</div>
    </div>
    <div class="foot">
      <span>
        <WatchIcon class="icon" size="1x" />
        {{$time(comment.createdAt)}}
      </span>
      <span>
        <ThumbsUpIcon class="icon" size="1x" />
        {{comment.thumbupCount}}
      </span>
    </div>
  </div>
</template>
<script>
import { WatchIcon, ThumbsUpIcon, MessageCircleIcon } from "vue-feather-icons";

export default {
  components: {
    WatchIcon,
    ThumbsUpIcon,
    MessageCircleIcon
  },
  props: {
    comment: {
      type: Object
    }
  }
};
</script>
<style lang="scss">
.cmt {
  padding: 12px 20px 19px;
  border-bottom: 1px solid #eee;
  &.reply {
    margin-top: -1px;
    border-top: 1px solid #eee;
    background-color: #f8f8f8;
    padding-left: 40px;
  }
  .head {
    margin-top: 9px;
    color: #94969b;
    font-size: 12px;
    line-height: 1.33em;
  }
  .content {
    white-space: pre-line;
    padding: 10px 0;
  }
  .foot {
    margin-top: 10px;
    opacity: 0.4;
    display: flex;
    gap: 20px;
    font-size: 14px;
    .icon {
      position: relative;
      top: 1.5px;
      margin-right: 5px;
    }
  }
}
</style>
