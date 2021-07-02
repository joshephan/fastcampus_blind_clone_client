<template>
  <div class="main-container">
    <main>
      <Searchbar />
      <BestBoardCard v-if="mainContent[0]" :articleList="mainContent[0].content" />
      <div class="board-card-container">
        <BoardCard
          v-for="b in mainContent"
          :key="b.slug"
          :title="b.title"
          :slug="b.slug"
          :articleList="b.content"
        />
      </div>
    </main>
    <RealtimeFamousCompany />
  </div>
</template>
<script>
import BestBoardCard from "@/components/Main/BestBoardCard";
import BoardCard from "@/components/Main/BoardCard";
import RealtimeFamousCompany from "@/components/Main/RealtimeFamousCompany";

export default {
  components: {
    BestBoardCard,
    BoardCard,
    RealtimeFamousCompany
  },
  data() {
    return {
      mainContent: []
    };
  },
  created() {
    this.getRecentBoardArticleList();
  },
  methods: {
    async getRecentBoardArticleList() {
      const data = await this.$api.$get("/main");

      if (data.error) {
        return;
      }

      this.mainContent = data.content;
    }
  }
};
</script>
<style lang="scss">
.main-container {
  display: flex;
  margin: auto;
  width: 100%;
  max-width: 1100px;
  main {
    width: 100%;
    max-width: 736px;
  }
}
.board-card-container {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 45px 40px;
}
</style>
