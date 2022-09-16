<template>
  <el-scrollbar height="660px">
    <div class="article-page">
      <p class="article-header">
        {{ articleVal }}
      </p>
      <div class="author-info">
        <el-avatar
          size="40"
          src="http://localhost:8888/assets/img/avatar/B4D71E638C97A179DB671942B241E59B.webp"
          style="--el-avatar-size: 39px"
          class="author-info-avatar"
        />
        <div class="author-info-name-and-time">
          <div class="name">{{ !authorName ? "游客" : authorName }}</div>
          <div class="time">{{ articleStandardTime }}</div>
        </div>
        <div class="author-msg">个人账号</div>
      </div>
      <div class="article-content">
        {{ articleVal }}
      </div>
      <div class="article-talk">
        <div class="article-talk-header">发表评论</div>
        <el-input
          v-model="textarea"
          maxlength="200"
          placeholder="请输入评论"
          show-word-limit
          type="textarea"
          rows="5"
          class="talkTextArea"
        />
        <el-button type="primary" class="talk-btn" @click="postTalk"
          >发表</el-button
        >
      </div>
      <div class="talk-lists">
        <div class="talk-lists-header">评论列表</div>
        <ArticleTlakItem
          v-for="talkItem in talkLists"
          :key="talkItem.id"
          :talkItem="talkItem"
        />
      </div>
    </div>
  </el-scrollbar>
</template>

<script>
import { reactive, ref } from "vue";
// import router from "../router";
import { nanoid } from "nanoid";
import moment from "moment";
import ArticleTlakItem from "../components/ArticleTlakItem.vue";
import store from "@/store";

export default {
  name: "ArticleDetailPage",
  components: {
    ArticleTlakItem,
  },
  props: ["articleId", "articleTime", "articleVal"], // 路由传来的
  setup(props) {
    const textarea = ref("");
    let talkLists = reactive(store.state.articleTalk.articleTalkArr);
    const articleStandardTime = ref(
      moment(parseInt(props.articleTime)).format("YYYY-MM-DD HH:mm:ss")
    );
    const authorName = ref(localStorage.getItem("account"));

    function postTalk() {
      let talkItem = {
        id: nanoid(),
        content: textarea.value,
        time: Date.now(),
      };
      textarea.value = "";
      store.dispatch("articleTalk/addTalk", talkItem);
    }

    return {
      articleStandardTime,
      textarea,
      talkLists,
      postTalk,
      authorName,
    };
  },
};
</script>

<style scoped>
.article-page {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 666px;
  overflow: auto;
}
.article-header {
  padding: 10px 0px 10px;
  font-weight: 900;
  font-size: 26px;
  margin-bottom: 20px;
}
.author-info {
  display: flex;
  flex-direction: row;
  height: 55px;
  padding: 0 10px 20px;
  justify-content: flex-start;
  align-items: center;
}
.author-info-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin-right: 20px;
}

.author-info-name-and-time {
  margin-right: 10px;
}
.time {
  padding: 0;
  font-family: PingFangSC-Regular;
  font-size: 13px;
  color: #9195a3;
}
.author-msg {
  position: relative;
  top: 10px;
  font-size: 13px;
  color: #9195a3;
}
.article-content {
  line-height: 25px;
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
  padding: 25px 20px;
  color: #000;
}
.article-talk {
  margin: 30px 0;
}
.article-talk-header {
  font-family: PingFangSC-Semibold;
  font-size: 18px;
  line-height: 1;
  color: #000;
  margin-bottom: 30px;
}
.talk-btn {
  position: relative;
  left: 566px;
  top: 5px;
  width: 100px;
}

.talk-lists {
  margin: 0;
}
.talk-lists-header {
  font-family: PingFangSC-Semibold;
  font-size: 18px;
  line-height: 1;
  color: #000;
  margin-bottom: 30px;
}
</style>
