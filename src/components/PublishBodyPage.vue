<template>
  <div class="publish-body-container">
    <el-scrollbar height="565px">
      <PublishItem
        v-for="articleItem in articleLists"
        :key="articleItem.id"
        :articleItem="articleItem"
      />
    </el-scrollbar>
  </div>
</template>
<script>
// import { onBeforeUnmount, onMounted } from "vue";
// import router from "../router";
import PublishItem from "./PublishItem.vue";

export default {
  name: "PublishBodyPage",
  props: ["articleLists"],
  components: {
    PublishItem,
  },
  setup() {},
};
</script>
<style scoped>
.publish-body-container {
  display: flex;
  flex-direction: column;
  border: 1px solid #ccc;
  height: 570px;
  width: 830px;
  overflow: auto;
}
</style>
