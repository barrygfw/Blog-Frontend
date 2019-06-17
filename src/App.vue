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
              <router-link to="/login"><el-menu-item index="4">登录</el-menu-item></router-link>
            </el-menu>
          </div>
        </el-col>
        <el-col :span="14" :offset="5">
          <router-view/>
        </el-col>
      </el-row>
    </div>
</template>

<script>
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
