<template>
  <el-form
    :rules="rules"
    class="login-container"
    label-position="left"
    label-width="0px"
    v-loading="loading"
  >
    <h3 class="login_title">系统注册</h3>
    <el-form-item>
      <el-input
        type="text"
        v-model="registerForm.user_name"
        auto-complete="off"
        placeholder="用户名"
      >
        <template slot="prepend"
          >用户名</template
        ></el-input
      >
    </el-form-item>
    <el-form-item>
      <el-input
        type="password"
        v-model="registerForm.password"
        auto-complete="off"
        placeholder="密码"
      >
        <template slot="prepend"
          >密码</template
        ></el-input
      >
    </el-form-item>
    <el-form-item>
      <el-input
        type="password"
        v-model="registerForm.repassword"
        auto-complete="off"
        placeholder="密码"
      >
        <template slot="prepend"
          >再次输入密码</template
        ></el-input
      >
    </el-form-item>
    <el-form-item>
      <el-input
        type="password"
        v-model="registerForm.email"
        auto-complete="off"
        placeholder="邮箱"
      >
        <template slot="prepend"
          >邮箱</template
        ></el-input
      >
    </el-form-item>
    <el-form-item style="width: 100%">
      <el-button type="primary" @click="register" style="width: 100%"
        >注册</el-button
      >
      <br />
      <el-button @click="goHome" type="primary" style="width: 100%"
        >主界面</el-button
      >
    </el-form-item>
  </el-form>
</template>
<script>
  import { postRequest } from '../utils/api';
  export default {
    name: 'register',
    data() {
      return {
        rules: {},
        checked: true,
        registerForm: {
          user_name: '',
          password: '',
          repassword: '',
          email: '',
        },
        loading: false,
      };
    },
    methods: {
      goHome() {
        this.$router.push({ path: '/' });
      },
      test() {
        if (this.registerForm.password !== this.registerForm.repassword) {
          this.$message({ type: 'warning', message: '两次密码不一样!' });
          return false;
        } else if (!this.registerForm.user_name) {
          this.$message({ typr: 'warning', message: '请输入用户名!' });
          return false;
        } else if (!this.registerForm.email) {
          this.$message({ typr: 'warning', message: '请输入邮箱!' });
          return false;
        } else {
          return true;
        }
      },
      register() {
        if (this.test()) {
          let { email, user_name, password } = this.registerForm;
          let data = {
            email,
            user_name,
            password,
          };
          postRequest('/regist', data)
            .then(res => {
              if (res.data.status === '200') {
                this.$message({ type: 'success', message: '注册成功' });
                this.$router.push({ path: '/' });
              } else {
                this.$message({ typr: 'error', message: res.data.message });
              }
            })
            .catch(err => {
              this.$message({ typr: 'warning', message: '请检查输入!' });
            });
        } else {
          this.$message({ typr: 'warning', message: '请检查输入!' });
        }
      },
    },
  };
</script>
<style>
  .login-container {
    border-radius: 15px;
    background-clip: padding-box;
    margin: 180px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }

  .login_title {
    margin: 0px auto 40px auto;
    text-align: center;
    color: #505458;
  }

  .login_remember {
    margin: 0px 0px 35px 0px;
    text-align: left;
  }
</style>
