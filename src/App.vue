<template>
    <div id="app" style="background-color: rgba(235, 235, 235, 0.08)">
      <el-row>
        <el-col :span="14" :offset="5">
          <div>
              <el-menu
                :default-active="activeIndex"
                class="el-menu-demo"
                mode="horizontal"
                @select="handleSelect"
              >
                <router-link to="/"><el-menu-item index="1">首页</el-menu-item></router-link>
                <router-link to="/category"><el-menu-item index="2">分类</el-menu-item></router-link>
                <router-link to="/author"><el-menu-item index="3">作者</el-menu-item></router-link>
              </el-menu>
            </div>
          </el-col>
      </el-row>
      <router-view/>
    </div>
</template>

<script>
import { getRequest } from './utils/api.js';
export default {
  name: 'app',
  data() {
      return {
        activeIndex: '1',
        activeIndex2: '1',
      };
    },
    methods: {
      handleSelect(key, keyPath) {
        // console.log(key, keyPath);
      },
      init() {
        let param = { state: 1, uid: 0, keywords: '', page: 1, page_size: 8 };
        getRequest('/article/all', param)
        .then(res => {
          console.log(res);
        })
        .catch(err => {
          // this.$alert(err);
          console.log(err);
        });
      }
    },
    created() {
      this.init();
    },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
