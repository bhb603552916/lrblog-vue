<template>
  <div class="hot-wrapper">
    <el-card>
      <div slot="header" class="header">
        <i class="iconfont icon-hotfill" style="margin-right: 5px; color: #ff5722;"></i>
        热门文章
      </div>
      <div v-if="hotArticleList.length > 0">
        <div class="hot-title" v-for="(tit, index) in hotArticleList" :key="tit.id">
          <i class="number">{{ index + 1 }}</i>
          <router-link :to="`/article/${tit.id}`">
            <span class="title">{{ tit.title | filterTitle(24) }}</span>
          </router-link>
        </div>
      </div>
      <skeleton-paragraph v-else class="content" :lines="10" line-height="1.2em" />
    </el-card>
  </div>
</template>

<script>
import ArticleApi from '@/model/article'

export default {
  name: 'hotArticleList',
  data() {
    return {
      hotArticleList: [],
    }
  },
  created() {
    this.gethotArticleList()
  },
  methods: {
    // 获取热门文章列表
    async gethotArticleList() {
      const hot_list = await ArticleApi.gethotArticleList()
      this.hotArticleList = hot_list.data
    },
  },
  // props: {
  //   hotArticleList: {
  //     type: Array,
  //   },
  // },
}
</script>

<style scoped lang="scss">
.hot-wrapper {
  // margin-top: 20px;
  width: 100%;
  .header {
    font-size: 14px;
    font-weight: bold;
  }
  .hot-title {
    text-align: left;
    line-height: 30px;
    font-size: 14px;
    .number {
      display: inline-block;
      width: 18px;
      height: 18px;
      line-height: 18px;
      margin-right: 20px;
      text-align: center;
      font-size: 12px;
      background: rgba(197, 197, 197, 0.6);
    }
    .title {
      cursor: pointer;
      transition: margin 0.25s;
    }
    .title:hover {
      color: $theme;
      margin-left: 10px;
      text-decoration: underline;
    }
    .title {
      cursor: pointer;
    }
  }
  .hot-title:nth-child(1) .number {
    background: rgba(250, 10, 10, 0.6);
    color: white;
  }
  .hot-title:nth-child(2) .number {
    background: rgba(255, 136, 0, 0.66);
    color: white;
  }
  .hot-title:nth-child(3) .number {
    background: rgba(41, 179, 168, 0.6);
    color: white;
  }
}
</style>
