<template>
  <div class="wrap-searchbar">
    <SearchIcon class="search-icon" />
    <input type="text" v-model="query" placeholder="관심있는 내용을 검색해보세요!" />
  </div>
</template>
<script>
import { SearchIcon } from "vue-feather-icons";
export default {
  components: {
    SearchIcon
  },
  data() {
    return {
      query: null
    };
  }
};
</script>
<style lang="scss" scoped>
.wrap-searchbar {
  width: 100%;
  margin: 40px 0 20px;
  & > .search-icon {
    position: absolute;
    margin-left: 20px;
    margin-top: 18px;
  }
  & > input {
    display: block;
    width: inherit;
    height: 60px;
    padding: 0 10px 0 62px;
    border: 2px solid #222;
    font-size: 18px;
    border-radius: 30px;
    box-sizing: border-box;
  }
}
</style>
