<template>
  <el-row>
    <el-col :span="24">
      <br />
      <el-card shadow="hover">
        <div slot="header">
          <p style="display:flex;justify-content:space-between;">
            <span>{{ article.editTime | formatDateTime }}</span>
            <span
              ><b>{{ article.title }}</b></span
            >
            <span>{{ article.user_name }}</span>
          </p>
        </div>
        <div style="text-align: left" v-html="article.htmlContent"></div>
      </el-card>
    </el-col>
  </el-row>
</template>
<script>
  import { getRequest } from '../utils/api.js';

  export default {
    name: 'detail',
    data() {
      return {
        article: '',
      };
    },
    methods: {
      init() {
        getRequest(`/article/${this.$route.query.id}`)
          .then(res => {
            this.article = res.data.data;
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
