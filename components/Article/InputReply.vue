<template>
  <div id="input-comment">
    <CameraIcon class="icon" />
    <div class="content-container">
      <textarea v-model="content" placeholder="대댓글을 남겨주세요."></textarea>
      <div class="foot">
        <a @click.prevent="$emit('close')">취소</a>
        <a
          :class="[content !== null && content !== '' && 'active']"
          @click.prevent="uploadComment"
        >등록</a>
      </div>
    </div>
  </div>
</template>
<script>
import { CameraIcon } from "vue-feather-icons";
export default {
  components: {
    CameraIcon
  },
  props: {
    commentId: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      content: null
    };
  },
  methods: {
    async uploadComment() {
      const data = await this.$api.$post("/reply/create", {
        comment: this.commentId,
        content: this.content,
      });
      if (!data) {
        return;
      }
      this.content = null;
      this.$emit('close');
    }
  }
};
</script>
<style lang="scss" scoped>
#input-comment {
  display: flex;
  padding: 20px;
  border: 1px solid #d4d4d4;
  .icon {
    margin-right: 20px;
  }
  .empty {
    line-height: 28px;
    cursor: pointer;
  }
  .content-container {
    width: 100%;
  }
  textarea {
    resize: none;
    width: 100%;
    display: block;
    border: none;
    font-size: 16px;
    min-height: 100px;
    margin-bottom: 20px;
  }
  .foot {
    display: flex;
    justify-content: flex-end;
    gap: 20px;
    a {
      color: #d4d4d4;
      &.active {
        color: #222222;
      }
    }
  }
}
</style>
