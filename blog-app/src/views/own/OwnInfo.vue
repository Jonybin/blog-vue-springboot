<template>
  <div v-title data-title="Topcoder">
    <el-container>
      <el-main class="me-articles">
        <article-scroll-page></article-scroll-page>
      </el-main>

      <el-aside>
        <!-- <card-me class="me-area"></card-me> -->
        <card-advertise :advertise="advertise" class="me-area"></card-advertise>
        <card-tag :tags="hotTags"></card-tag>

        <card-article cardHeader="最热文章" :articles="hotArticles"></card-article>

        <card-archive cardHeader="文章归档" :archives="archives"></card-archive>

        <card-article cardHeader="最新文章" :articles="newArticles"></card-article>
      </el-aside>
    </el-container>
  </div>
</template>

<script>
import CardMe from "@/components/card/CardMe";
import Advertise from "@/components/card/Advertise";
import CardArticle from "@/components/card/CardArticle";
import CardArchive from "@/components/card/CardArchive";
import CardTag from "@/components/card/CardTag";
import ArticleScrollPage from "@/views/common/ArticleScrollPage";

import {
  getArticles,
  getHotArtices,
  getNewArtices,
  getAdvertise
} from "@/api/article";
import { getHotTags } from "@/api/tag";
import { listArchives } from "@/api/article";

export default {
  name: "Index",
  created() {
    this.getHotArtices();
    this.getNewArtices();
    this.getHotTags();
    this.listArchives();
    this.getAdvertise();
  },
  data() {
    return {
      hotTags: [],
      hotArticles: [],
      newArticles: [],
      archives: [],
      advertise: [
        {
          src:
            "http://a0.att.hudong.com/05/18/01200000194499134433185504843.jpg",
          title: "ceshi"
        }
      ]
    };
  },
  methods: {
    getHotArtices() {
      let that = this;
      getHotArtices()
        .then(data => {
          that.hotArticles = data.data;
        })
        .catch(error => {
          if (error !== "error") {
            that.$message({
              type: "error",
              message: "最热文章加载失败!",
              showClose: true
            });
          }
        });
    },
    getNewArtices() {
      let that = this;
      getNewArtices()
        .then(data => {
          that.newArticles = data.data;
        })
        .catch(error => {
          if (error !== "error") {
            that.$message({
              type: "error",
              message: "最新文章加载失败!",
              showClose: true
            });
          }
        });
    },
    getHotTags() {
      let that = this;
      getHotTags()
        .then(data => {
          that.hotTags = data.data;
        })
        .catch(error => {
          if (error !== "error") {
            that.$message({
              type: "error",
              message: "最热标签加载失败!",
              showClose: true
            });
          }
        });
    },
    listArchives() {
      let that = this;
      listArchives()
        .then(data => {
          this.archives = data.data;
        })
        .catch(error => {
          if (error !== "error") {
            that.$message({
              type: "error",
              message: "文章归档加载失败!",
              showClose: true
            });
          }
        });
    },
    getAdvertise() {
      let that = this;
      getAdvertise()
        .then(data => {
          this.advertise = data.data;
        })
        .catch(error => {});
    }
  },
  components: {
    "card-advertise": Advertise,
    "card-me": CardMe,
    "card-article": CardArticle,
    "card-tag": CardTag,
    ArticleScrollPage,
    CardArchive
  }
};
</script>

<style scoped>
.el-container {
  width: 960px;
}

.el-aside {
  margin-left: 20px;
  width: 260px;
}

.el-main {
  padding: 0px;
  line-height: 16px;
}

.el-card {
  border-radius: 0;
}

.el-card:not(:first-child) {
  margin-top: 20px;
}
</style>
