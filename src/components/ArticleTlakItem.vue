<template>
  <div class="talk-item-container">
    <div class="item-name">
      游客{{ talkItem && talkItem.id.substring(0, 5) }}
    </div>
    <div class="item-content">
      {{ talkItem && talkItem.content }}
    </div>
    <div class="item-time">{{ timeText }}</div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import moment from "moment";

export default {
  name: "ArticleTlakItem",
  props: ["talkItem"],
  setup(props) {
    let timeText = ref("");
    let talkTime = ref("");
    onMounted(() => {
      timeText.value = moment(props.talkItem.time).format(
        "YYYY-MM-DD HH:mm:ss"
      );
    });
    // watch(talkTime, () => {
    //   talkTime.value = Date.now() - props.talkItem.time;
    //   if (talkTime.value < 240000) {
    //     timeText.value = "30秒前";
    //   } else {
    //     timeText.value = moment(props.talkItem.time).format(
    //       "YYYY-MM-DD HH:mm:ss"
    //     );
    //   }
    // });
    return {
      talkTime,
      timeText,
    };
  },
};
</script>

<style scoped>
/*item*/
.talk-item-container {
  display: flex;
  flex-direction: column;
  width: 666px;
  margin-bottom: 20px;
}
.item-name {
  font-weight: 700;
  font-size: 13px;
  color: #222;
}
.item-content {
  padding: 10px;
  font: 14px/22px PingFangSC-Regular;
  color: #222;
  text-align: justify;
  word-wrap: break-word;
  word-break: break-all;
  word-break: break-word;
}
.item-time {
  padding: 0 8px;
  font-family: PingFangSC-Regular;
  font-size: 13px;
  color: #9195a3;
}
</style>
