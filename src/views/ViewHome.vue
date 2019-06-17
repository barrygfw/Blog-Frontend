<template>
  <el-row>
    <h3>{{ this.$route.query.userName }}</h3>
    <el-col :span="11" :offset="1" v-for="item in list" :key="item.id">
      <el-card class="box-card" shadow="hover">
        <div slot="header" class="clearfix">
          <span>{{ item.cateName }}</span>
          <el-button
            @click="showDetail(item.id)"
            style="float: right; padding: 3px 0"
            type="text"
            >查看详情</el-button
          >
        </div>
        <div class="text item title">
          {{ item.title }}
        </div>
        <p style="font-size:14px;">{{ item.editTime | formatDateTime }}</p>
      </el-card>
    </el-col>
  </el-row>
</template>
<script>
  import { getRequest } from '../utils/api.js';

  export default {
    name: 'viewHome',
    data() {
      return {
        list: [],
        pageSize: 8,
      };
    },
    methods: {
      showDetail(id) {
        this.$router.push({ path: '/detail', query: { id } });
      },
      init() {
        if (this.$route.query.authorId) {
          getRequest(
            `/article/all?state=1&keywords&cid=0&uid=${
              this.$route.query.authorId
            }&page=1&page_size=${this.pageSize}&cid=0`
          )
            .then(res => {
              this.list = res.data.data.articles;
            })
            .catch(err => {
              console.log(err);
            });
        } else if (this.$route.query.categoryId) {
          getRequest(
            `/article/all?state=1&keywords=&uid=0&page=1&cid=${
              this.$route.query.categoryId
            }&page_size=${this.pageSize}`
          )
            .then(res => {
              this.list = res.data.data.articles;
            })
            .catch(err => {
              console.log(err);
            });
        } else {
          getRequest(
            `/article/all?state=1&keywords=&uid=0&cid=0&page=1&page_size=${
              this.pageSize
            }`
          )
            .then(res => {
              this.list = res.data.data.articles;
            })
            .catch(err => {
              console.log(err);
            });
        }
      },
    },
    created() {
      this.init();
    },
  };
</script>
<style scoped>
  .text {
    font-size: 14px;
  }

  .title {
    font-size: 17px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: '';
  }
  .clearfix:after {
    clear: both;
  }

  .box-card {
    margin-top: 20px;
  }
</style>
