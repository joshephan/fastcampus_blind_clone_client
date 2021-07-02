<template>
  <div class="board-container">
    <section>
      <strong>{{query}}</strong>
      검색결과
    </section>
    <section class="total">전체({{articleList.length}})</section>
    <section class="article-list">
      <GlobalArticleCard v-for="a in articleList" :article="a" :key="a._id" />
      <infinite-loading @infinite="findSearchResult"></infinite-loading>
    </section>
  </div>
</template>
<script>
export default {
  data() {
    return {
      query: null,
      articleList: [],
      lastIndex: 0
    };
  },
  methods: {
    findSearchResult($state) {
      setTimeout(async () => {
        if (this.articleList.length > 0) {
          this.lastIndex = this.articleList[this.articleList.length - 1]._id;
        }

        this.query = this.$route.params.query;
        const data = await this.$api.$get(
          `/search/${this.query}?lastIndex=${this.lastIndex}`
        );
        if (data.article.length === 0) {
          $state.complete();
        } else {
          this.articleList = this.articleList.concat(data.article);
          $state.loaded();
        }
      }, 300);
    }
  }
};
</script>
