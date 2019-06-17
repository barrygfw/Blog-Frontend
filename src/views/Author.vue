<template>
  <el-row>
    <br />
    <el-col :span="11" :offset="1" v-for="item in authors" :key="item.id">
      <el-card class="box-card" shadow="hover">
        <div slot="header" class="clearfix">
          <span>用户名:{{ item.user_name }}</span>
          <el-button
            @click="showArticles(item.id, item.user_name)"
            style="float: right; padding: 3px 0"
            type="text"
            >查看文章</el-button
          >
        </div>
        <div class="text item title">
          {{ item.title }}
        </div>
        <p style="font-size:14px;"><b>Email:</b>{{ item.email }}</p>
      </el-card>
      <br />
    </el-col>
  </el-row>
</template>
<script>
  import { getRequest } from '../utils/api.js';

  export default {
    name: 'author',
    data() {
      return {
        authors: [],
      };
    },
    methods: {
      showArticles(id, userName) {
        this.$router.push({ path: '/', query: { authorId: id, userName } });
      },
      init() {
        getRequest('/user/findAll')
          .then(res => {
            this.authors = res.data;
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
