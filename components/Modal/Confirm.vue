<template>
  <div v-if="show" class="modal-outside">
    <div id="confirm-modal">
      <div class="title">{{title}}</div>
      <div class="btn-container">
        <button class="cancel btn" @click="$emit('confirm', false)">취소</button>
        <button class="confirm btn" @click="$emit('confirm', true)">{{confirmBtnText}}</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
      default: "",
      required: true
    },
    confirmBtnText: {
      type: String,
      default: "확인"
    }
  }
};
</script>
<style lang="scss" scoped>
#confirm-modal {
  width: 320px;
  padding: 24px;
  background: white;
  .btn-container {
    display: flex;
    margin-top: 30px;
  }
}
</style>
