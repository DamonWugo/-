<template>
  <li>
    {{ seachArticleItem.val }}
  </li>
</template>

<script>
import { onMounted } from "vue";

export default {
  name: "PublishItem",
  //声明接收 父组件 MyList传来的数据
  props: ["seachArticleItem"],
  setup(props) {
    onMounted(() => {
      console.log("[]", props.seachArticleItem);
    });
  },
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 30px;
  width: 250px;
  line-height: 30px;
  padding: 0 20px;
  border: 1px solid #ddd;
  cursor: pointer;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

li:hover {
  background-color: #ddd;
}
</style>
