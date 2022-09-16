<template>
  <div class="publish-container">
    <div class="publish-left">
      <ClassicPage :articleLists="articleLists" />
    </div>
    <div class="publish-mid">
      <div class="publish-header">
        <div class="todo-header">
          <span class="publish-logo">主贴</span>
          <input
            type="text"
            placeholder="请输入你的帖子内容，按回车键确认"
            @keyup.enter="postArticle"
            v-model="articleContent"
            @focus="getInputValue"
          />
        </div>
        <el-button type="primary" @click="postArticle" class="postBtn"
          >发&nbsp;布</el-button
        >
      </div>
      <PublishBodyPage :articleLists="articleLists"></PublishBodyPage>
    </div>
    <div class="publish-right">
      <KeyWordSearch :articleLists="articleLists"></KeyWordSearch>
    </div>
  </div>
</template>
<script>
// import router from "../router";
import PublishBodyPage from "../components/PublishBodyPage.vue";
import KeyWordSearch from "../components/KeyWordSearch.vue";
import ClassicPage from "../components/ClassicPage.vue";
import { reactive, ref } from "vue";
import { nanoid } from "nanoid";
import store from "@/store";

export default {
  name: "PublishPage",
  components: {
    PublishBodyPage,
    KeyWordSearch,
    ClassicPage,
  },
  setup() {
    const articleLists = reactive(store.state.articlePublish.articlePublishArr);
    let articleContent = ref("");
    function postArticle() {
      if (articleContent.value.indexOf("#") === -1) {
        alert("请输入分类");
        return;
      }
      const articleItem = {
        val: articleContent.value.split("#")[1],
        id: nanoid(),
        type:
          articleContent.value.split("#")[0] !== ""
            ? articleContent.value.split("#")[0]
            : "其他",
        time: Date.now(),
      };
      articleContent.value = "";
      //   articleLists.unshift(articleItem);
      store.dispatch("articlePublish/addArticle", articleItem);
    }

    return {
      articleContent,
      articleLists,
      postArticle,
    };
  },
};
</script>
<style scoped>
.publish-container {
  display: flex;
  flex-direction: row;
  margin: 0 auto;
  margin: 13px 23px;
}
.publish-header {
  display: flex;
  flex-direction: row;
  width: 830px;
  height: 50px;
  background-color: #79bbff;
  align-items: center;
  justify-content: flex-start;
}
.publish-logo {
  display: inline-block;
  color: #fff;
  font-weight: 700;
  font-size: 20px;
  margin: 0px 16px;
  height: 36px;
}
.todo-header input {
  width: 630px;
  height: 36px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
.postBtn {
  padding: 0;
  width: 100px;
  height: 36px;
  line-height: 33px;
  background-color: #fff;
  color: #409eff;
  font-weight: 700;
  font-size: 18px;
  margin-left: 8px;
}
.publish-left {
  width: 300px;
  height: 300px;
}
.publish-mid {
  display: flex;
  margin: 0 20px;
  flex-direction: column;
}
.publish-right {
  width: 300px;
  height: 300px;
}
</style>
