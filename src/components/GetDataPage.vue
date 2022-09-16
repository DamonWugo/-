<template>
  <div class="get-data-container">
    <div>共有{{ articleLists.length }}</div>
    <div class="get-data-biao">点击导出数据表格</div>
  </div>
</template>
<script>
// import { reactive } from "vue";
// import router from "../router";
export default {
  name: "GetDataPage",
  props: ["articleLists"],
  components: {},
  setup() {
    return {};
  },
};
</script>
<style scoped>
.get-data-container {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  margin-top: 20px;
  border: 1px solid #ccc;
  width: 300px;
  height: 77px;
  padding: 10px;
}
.get-data-biao {
  color: #79bbff;
  cursor: pointer;
}
</style>
