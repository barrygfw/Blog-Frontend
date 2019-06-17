<template>
  <el-row>
    <br />
    <el-col :span="11" :offset="1" v-for="item in categorys" :key="item.id">
      <el-card class="box-card" shadow="hover">
        <div slot="header" class="clearfix">
          <span>{{ item.cateName }}</span>
          <el-button
            @click="showArticles(item.id)"
            style="float: right; padding: 3px 0"
            type="text"
            >查看文章</el-button
          >
        </div>
        <div class="text item title">
          {{ item.date | formatDateTime }}
        </div>
      </el-card>
      <br />
    </el-col>
  </el-row>
</template>
<script>
  import { getRequest } from '../utils/api.js';

  export default {
    name: 'category',
    data() {
      return {
        categorys: [],
      };
    },
    methods: {
      showArticles(id) {
        this.$router.push({ path: '/', query: { categoryId: id } });
      },
      init() {
        getRequest('/cate/all')
          .then(res => {
            this.categorys = res.data.data;
          })
          .catch(err => {
            console.log(err);
          });
      },
    },
    created() {
      this.init();
    },
  };
</script>
