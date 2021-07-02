<template>
  <article>
    <div class="head">
      <nuxt-link
        :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
        class="title"
      >{{article.title}}</nuxt-link>
    </div>
    <div class="body">
      <nuxt-link
        :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
        class="content"
      >{{article.content}}</nuxt-link>
      <div class="info">
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
          class="company"
        >{{article.author.company.name}}</nuxt-link>
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
        >·</nuxt-link>
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
          class="nickname"
        >{{article.author.nickname}}</nuxt-link>
      </div>
    </div>
    <div class="foot">
      <div class="left">
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
          class="count"
        >
          <EyeIcon class="icon" size="1x" />
          {{article.viewCount}}
        </nuxt-link>
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
          class="count"
        >
          <ThumbsUpIcon class="icon" size="1x" />
          {{article.thumbupCount}}
        </nuxt-link>
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
          class="count"
        >
          <MessageCircleIcon class="icon" size="1x" />
          {{article.commentCount}}
        </nuxt-link>
      </div>
      <div class="right">
        <nuxt-link
          :to="{
        name: 'post-key',
        params: {
          key: article.key
        }
      }"
        >{{$time(article.createdAt)}}</nuxt-link>
        <BookmarkIcon class="icon" size="1x" />
      </div>
    </div>
  </article>
</template>
<script>
import {
  EyeIcon,
  ThumbsUpIcon,
  MessageCircleIcon,
  BookmarkIcon
} from "vue-feather-icons";

export default {
  props: {
    article: {
      type: Object
    }
  },
  components: { EyeIcon, ThumbsUpIcon, MessageCircleIcon, BookmarkIcon }
};
</script>
<style lang="scss">
article {
  padding: 20px;
  border-bottom: 1px solid #eee;
  a {
    color: #222;
  }
  &:nth-child(2n - 1) {
    border-right: 1px solid #eee;
  }
  .head {
    .title {
      display: block;
      font-weight: bold;
      font-size: 18px;
      line-height: 1.4em;
      margin-top: 1px;
      height: 52px;
      margin-bottom: 0;
    }
  }
  .body {
    .content {
      margin-top: 4px;
      color: #222;
      display: block;
      font-size: 14px;
      line-height: 1.25em;
    }
    .info {
      margin-top: 20px;
      display: block;
    }
  }
  .foot {
    display: flex;
    margin-top: 8px;
    justify-content: space-between;
    opacity: 0.4;
    .count {
      margin-right: 15px;
      .icon {
        position: relative;
        top: 1px;
      }
    }
  }
}
</style>
