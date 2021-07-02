<template>
  <div class="board-container">
    <section v-if="boardList.length > 0" class="board">
      <nuxt-link
        v-for="b in boardList"
        :key="b._id"
        :class="['board-item', $route.params.id === b.slug && 'active']"
        :to="{
        name: 'topics-id',
        params: {
          id: b.slug
        }
      }"
      >{{b.title}}</nuxt-link>
    </section>
    <section class="article-list">
      <GlobalArticleCard v-for="a in articleList" :article="a" :key="a._id" />
      <infinite-loading @infinite="getBoardArticleList"></infinite-loading>
    </section>
  </div>
</template>
<script>
export default {
  data() {
    return {
      boardList: [],
      articleList: [],
      lastIndex: 0
    };
  },
  created() {
    this.getBoardList();
  },
  methods: {
    async getBoardList() {
      const data = await this.$api.$get("/board/list");
      this.boardList = data;
    },
    getBoardArticleList($state) {
      setTimeout(async () => {
        if (this.articleList.length > 0) {
          this.lastIndex = this.articleList[this.articleList.length - 1]._id;
        }

        const data = await this.$api.$get(
          `/board/${this.$route.params.id}?lastIndex=${this.lastIndex}`
        );
        if (data.article.length === 0) {
          $state.complete();
        } else {
          this.articleList = this.articleList.concat(data.article);
          $state.loaded();
        }
      }, 100);
    }
  }
};
</script>
