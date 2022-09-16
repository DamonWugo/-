<template>
  <div class="classic-container">
    <div class="classic-header">
      <div class="classic-left">
        <ul>
          <li
            v-for="(classicItem, index) in classicArr"
            :key="index"
            @click="getClassicItem(classicItem)"
          >
            {{ classicItem }}
          </li>
        </ul>
      </div>
      <div class="classic-right">
        <div v-if="!classicArticleLists">暂无符合条件数据</div>
        <div v-else>
          <el-scrollbar height="210px">
            <ClassicItem
              v-for="classicArticleItem in classicArticleLists"
              :key="classicArticleItem.id"
              :classicArticleItem="classicArticleItem"
            />
          </el-scrollbar>
        </div>
      </div>
    </div>
    <div class="classic-footer">
      <TuBiao :articleLists="articleLists" />
    </div>
    <div class="more-footer">
      <GetDataPage :articleLists="articleLists" />
    </div>
  </div>
</template>
<script>
import { reactive, ref } from "vue";
// import router from "../router";
import ClassicItem from "./ClassicItem.vue";
import TuBiao from "./ClassicTuBiao.vue";
import GetDataPage from "./GetDataPage.vue";
export default {
  name: "ClassicPage",
  props: ["articleLists"],
  components: {
    ClassicItem,
    TuBiao,
    GetDataPage,
  },
  setup(props) {
    const classicArr = reactive([
      "java",
      "C",
      "C++",
      "Python",
      "js",
      "Golong",
      "其他",
    ]);
    let classicArticleLists = ref("");
    function getClassicItem(classicItem) {
      classicArticleLists.value = props.articleLists.filter((item) => {
        return item.type === classicItem;
      });
      if (classicArticleLists.value.length === 0) {
        classicArticleLists.value = "";
      }
    }
    return {
      classicArticleLists,
      classicArr,
      getClassicItem,
    };
  },
};
</script>
<style scoped>
.classic-container {
  display: flex;
  flex-direction: column;
  height: 242px;
}
.classic-header {
  display: flex;
  flex-direction: row;
  height: 242px;
}
.classic-left {
  display: flex;
  flex-direction: column;
}
.classic-left ul li {
  width: 100px;
  height: 34px;
  line-height: 30px;
  border: 1px solid #ccc;
  background-color: #79bbff;
  text-align: center;
  cursor: pointer;
  color: #fff;
}
.classic-left ul li:hover {
  background-color: #fff;
  color: #79bbff;
}

.classic-right {
  width: 210px;
  height: 238px;
  border: 1px solid #ccc;
  overflow-y: auto;
}
</style>
