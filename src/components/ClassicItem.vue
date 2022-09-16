<template>
  <li>
    {{ classicArticleItem.val }}
  </li>
</template>

<script>
import { onMounted } from "vue";

export default {
  name: "ClassicItem",
  //声明接收 父组件 MyList传来的数据
  props: ["classicArticleItem"],
  setup(props) {
    onMounted(() => {
      console.log("[]", props.classicArticleItem);
    });
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 30px;
  line-height: 30px;
  padding: 0 20px;
  border: 1px solid #ddd;
  width: 198px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

li:hover {
  cursor: pointer;

  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>
