<template>
  <div class="classic-tubiao-container"></div>
</template>
<script>
import { onMounted, reactive, watch } from "vue";
// import router from "../router";
import * as echarts from "echarts";
export default {
  name: "TuBiao",
  props: ["articleLists"],
  components: {},
  setup(props) {
    let javaArr = reactive([]);
    let CArr = reactive([]);
    let CplusArr = reactive([]);
    let PythonArr = reactive([]);
    let GolongArr = reactive([]);
    let jsArr = reactive([]);
    onMounted(() => {
      props.articleLists.map((item) => {
        switch (item.type) {
          case "java":
            {
              javaArr.unshift(item);
            }
            break;
          case "C":
            {
              CArr.unshift(item);
            }
            break;
          case "C++":
            {
              CplusArr.unshift(item);
            }
            break;
          case "Python":
            {
              PythonArr.unshift(item);
            }
            break;
          case "Golong":
            {
              GolongArr.unshift(item);
            }
            break;
          case "js":
            {
              jsArr.unshift(item);
            }
            break;
        }
      });
      // 基于准备好的dom，初始化echarts实例
      var classicChart = echarts.init(
        document.querySelector(".classic-tubiao-container")
      );
      // 绘制图表
      classicChart.setOption({
        title: {
          text: " 帖子语言分类相关性分析",
        },
        tooltip: {},
        xAxis: {
          data: ["java", "C", "C++", "Python", "Golong", "js"],
        },
        yAxis: {},
        series: [
          {
            name: "讨论度",
            type: "bar",
            data: [
              javaArr.length,
              CArr.length,
              CplusArr.length,
              PythonArr.length,
              GolongArr.length,
              jsArr.length,
            ],
          },
        ],
      });
    });
    watch(props.articleLists, () => {
      javaArr = [];
      CArr = [];
      CplusArr = [];
      PythonArr = [];
      GolongArr = [];
      jsArr = [];
      props.articleLists.map((item) => {
        switch (item.type) {
          case "java":
            {
              javaArr.unshift(item);
            }
            break;
          case "C":
            {
              CArr.unshift(item);
            }
            break;
          case "C++":
            {
              CplusArr.unshift(item);
            }
            break;
          case "Python":
            {
              PythonArr.unshift(item);
            }
            break;
          case "Golong":
            {
              GolongArr.unshift(item);
            }
            break;
          case "js":
            {
              jsArr.unshift(item);
            }
            break;
        }
      });
      // 基于准备好的dom，初始化echarts实例
      var classicChart = echarts.init(
        document.querySelector(".classic-tubiao-container")
      );
      // 绘制图表
      classicChart.setOption({
        title: {
          text: " 语言分类相关性分析",
        },
        tooltip: {},
        xAxis: {
          data: ["java", "C", "C++", "Python", "Golong", "js"],
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [
              javaArr.length,
              CArr.length,
              CplusArr.length,
              PythonArr.length,
              GolongArr.length,
              jsArr.length,
            ],
          },
        ],
      });
    });
    return {
      javaArr,
      CArr,
      CplusArr,
      PythonArr,
      GolongArr,
      jsArr,
    };
  },
};
</script>
<style scoped>
.classic-tubiao-container {
  margin-top: 20px;
  border: 1px solid #ccc;
  padding: 30px 0px 0;
  height: 263px;
}
</style>
