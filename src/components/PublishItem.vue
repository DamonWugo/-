<template>
  <li @click="gotoArticleDel">
    <span class="text">{{ articleItem.val }}</span>
    <span class="item-classic">{{ articleItem.type }}</span>
    <span class="timer">发表于 {{ publishTime }}</span>
  </li>
</template>

<script>
import moment from "moment";
import router from "../router";
import { ref } from "vue";
export default {
  name: "PublishItem",
  //声明接收 父组件 MyList传来的数据
  props: ["articleItem"],
  setup(props) {
    let publishTime = ref(
      moment(parseInt(props.articleItem.time)).format("YYYY-MM-DD HH:mm:ss")
    );
    function gotoArticleDel() {
      router.push({
        name: "articledetailpage",
        params: {
          articleId: props.articleItem.id,
          articleTime: props.articleItem.time,
          articleVal: props.articleItem.val,
        },
      });
    }
    return {
      publishTime,
      gotoArticleDel,
    };
  },
};
</script>

<style scoped>
/*item*/
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  list-style: none;
  height: 45px;
  width: 828px;
  line-height: 45px;
  padding: 0 20px;
  border-bottom: 1px solid #ddd;
}
li .text {
  width: 480px;
  cursor: pointer;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

li:hover {
  background-color: #ddd;
}

.item-classic {
  border: 1px solid #79bbff;
  border-radius: 15%;
  color: #79bbff;
  font-size: 13px;
  width: 55px;
  height: 25px;
  line-height: 25px;
  text-align: center;
}

.timer {
  font-size: 14px;
  color: rgb(162, 162, 162);
}
</style>
