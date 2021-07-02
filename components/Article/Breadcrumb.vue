<template>
  <section class="breadcrumb">
    <nuxt-link
      :to="{
      name: 'topics-id',
      params: {
        id: slug
      }
    }"
    >토픽 > {{title}}</nuxt-link>
  </section>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    slug: {
      type: String,
      required: true
    }
  }
};
</script>
<style lang="scss" scoped>
.breadcrumb {
  padding: 40px 0 20px;
  & > a {
    font-size: 14px;
    font-weight: 700;
    line-height: 16px;
    color: #222;
  }
}
</style>
