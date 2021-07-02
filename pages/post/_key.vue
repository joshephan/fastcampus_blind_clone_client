<template>
  <div v-if="article !== null" class="main-container">
    <main>
      <Breadcrumb :title="article.board.title" :slug="article.board.slug" />
      <h1>{{article.title}}</h1>
      <div class="company">
        <span style="color: #37acc9;">{{article.author.company.name}}</span>
        <span>·</span>
        <span>{{article.author.nickname}}</span>
      </div>
      <div class="info">
        <div class="left">
          <span>
            <WatchIcon class="icon" size="1x" />
            {{$moment(article.createdAt).format("MM.DD")}}
          </span>
          <span>
            <EyeIcon class="icon" size="1x" />
            {{article.viewCount}}
          </span>
          <span>
            <MessageCircleIcon class="icon" size="1x" />
            {{article.commentCount}}
          </span>
        </div>
        <div class="right">
          <span>
            <BookmarkIcon class="icon" size="1x" />
          </span>
          <span>
            <MoreHorizontalIcon class="icon" size="1x" />
          </span>
        </div>
      </div>
      <div class="content">{{article.content}}</div>
      <picture v-if="article.articleImgAddress" class="article-image">
        <img
          :src="`https://blind-clone-coding.s3.ap-northeast-2.amazonaws.com/${article.articleImgAddress}`"
          :alt="article.articleImgAddress"
        />
      </picture>
      <div class="action">
        <div class="left">
          <span>
            <ThumbsUpIcon class="icon" size="1x" />
            {{article.thumbupCount}}
          </span>
          <span>
            <MessageCircleIcon class="icon" size="1x" />
            {{article.commentCount}}
          </span>
        </div>
      </div>
      <section class="comment">
        <h5>댓글 {{article.commentCount}}</h5>
        <InputComment :articleId="article._id" />
        <div class="comment-list">
          <CommentCard v-for="c in comment" :key="c._id" :comment="c" />
        </div>
      </section>
    </main>
    <RecommendArticleList />
  </div>
</template>
<script>
import Breadcrumb from "@/components/Article/Breadcrumb";
import CommentCard from "@/components/Article/CommentCard";
import CommentList from "@/components/Article/CommentList";
import ContentCard from "@/components/Article/ContentCard";
import InputComment from "@/components/Article/InputComment";
import RecommendArticleList from "@/components/Article/RecommendArticleList";
import {
  EyeIcon,
  WatchIcon,
  ThumbsUpIcon,
  MessageCircleIcon,
  BookmarkIcon,
  MoreHorizontalIcon
} from "vue-feather-icons";
export default {
  components: {
    Breadcrumb,
    CommentCard,
    CommentList,
    ContentCard,
    InputComment,
    RecommendArticleList,
    EyeIcon,
    WatchIcon,
    ThumbsUpIcon,
    MessageCircleIcon,
    BookmarkIcon,
    MoreHorizontalIcon
  },
  data() {
    return {
      key: null,
      article: null,
      comment: []
    };
  },
  created() {
    this.getArticle();
  },
  methods: {
    async getArticle() {
      this.key = this.$route.params.key;
      const data = await this.$api.$get(`/article/${this.key}`);
      this.article = data.article;
      this.comment = data.comment;
    }
  }
};
</script>
<style lang="scss" scoped>
h1 {
  font-size: 24px;
  margin: 0;
  line-height: 32px;
}
h5 {
  font-size: 16px;
}
.company {
  font-size: 14px;
  margin: 15px 0;
}
.info,
.action {
  opacity: 0.4;
  color: #222;
  display: flex;
  justify-content: space-between;
  padding-bottom: 20px;
  border-bottom: 1px solid #eee;
  .left,
  .right {
    display: flex;
    gap: 20px;
    .icon {
      position: relative;
      top: 1.5px;
    }
  }
}
.content {
  padding: 30px 0;
  white-space: pre-line;
  line-height: 28px;
}
</style>
