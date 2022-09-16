<template>
  <div class="key-word-search-container">
    <div class="key-header">
      <input type="text" class="key-input" v-model="seachKeyWordContent" />
      <button class="key-btn" @click="seachPosts">搜索</button>
    </div>
    <div class="key-body">
      <div v-if="!seachArticleLists">暂无符合条件数据</div>
      <div v-else>
        <el-scrollbar height="532px">
          <KeyWordSearchItem
            v-for="seachArticleItem in seachArticleLists"
            :key="seachArticleItem.id"
            :seachArticleItem="seachArticleItem"
          />
        </el-scrollbar>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
// import router from "../router";
import KeyWordSearchItem from "./KeyWordSearchItem.vue";

export default {
  name: "KeyWordSearch",
  props: ["articleLists"],
  components: {
    KeyWordSearchItem,
  },
  setup(props) {
    let seachKeyWordContent = ref("");
    let seachArticleLists = ref("");
    function seachPosts() {
      let tempVal = seachKeyWordContent.value;
      seachArticleLists.value = props.articleLists.filter((item) => {
        return item.val.indexOf(tempVal) > -1;
      });
      if (seachArticleLists.value.length === 0) {
        seachArticleLists.value = "";
      }
    }
    return {
      seachArticleLists,
      seachKeyWordContent,
      seachPosts,
    };
  },
};
</script>
<style scoped>
.key-word-search-container {
  display: flex;
  flex-direction: column;
  border: 1px solid #ccc;
  height: 620px;
  padding: 10px;
}
.key-header {
  display: flex;
  background-color: #fff;
}
.key-input {
  padding: 5px 10px;
  width: 200px;
  height: 30px;
  border: 1px solid #ccc;
  outline: 0;
  color: #757575;
}
.key-btn {
  width: 80px;
  height: 30px;
  background-color: #79bbff;
  color: #fff;
  font-weight: 700;
  font-size: 16px;
  cursor: pointer;
  border: 1px solid #79bbff;
}
.key-body {
  width: 280px;
  border: 1px solid #ccc;
  margin-top: 10px;
  padding: 10px;
  overflow-y: auto;
}
</style>
