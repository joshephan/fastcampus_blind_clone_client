<template>
  <div class="board-card">
    <div class="head">
      <div class="title-side">
        <div class="board-icon"></div>
        <h2>{{title}}</h2>
      </div>
      <nuxt-link
        :to="{
        name: 'topics-id',
        params: {
          id: slug
        }
      }"
      >더보기 ></nuxt-link>
    </div>
    <div class="body">
      <ul class="article-list">
        <li v-for="a in articleList" :key="a.id">
          <span class="article-title">{{a.title}}</span>
          <div class="count-display">
            <div class="count-item">
              <EyeIcon size="1x" class="icon" />
              {{a.viewCount}}
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import { EyeIcon } from "vue-feather-icons";

export default {
  props: {
    title: {
      type: String,
      required: true
    },
    slug: {
      type: String,
      required: true
    },
    articleList: {
      type: Array,
      default: []
    }
  },
  components: {
    EyeIcon
  }
};
</script>
<style lang="scss">
</style>
