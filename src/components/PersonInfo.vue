<template>
  <div>
    <br />
    <h3>更新个人信息</h3>
    <el-input placeholder="请修改用户名" v-model="user.user_name" size="mini">
      <template slot="prepend"
        >用户名</template
      >
    </el-input>
    <br /><br />
    <el-input placeholder="请修改密码" v-model="user.password" size="mini">
      <template slot="prepend"
        >密码</template
      >
    </el-input>
    <br /><br />
    <el-input placeholder="请修改邮箱" v-model="user.email" size="mini">
      <template slot="prepend"
        >邮箱</template
      >
    </el-input>
    <p style="display:flex;justify-content:space-around;">
      <el-button type="success" size="mini" @click="updatePersonInfo">
        更新
      </el-button>
    </p>
  </div>
</template>
<script>
  import { putRequest } from '../utils/api';

  export default {
    name: 'personInfo',
    data() {
      return {
        user: JSON.parse(sessionStorage.getItem('user')),
      };
    },
    methods: {
      updatePersonInfo() {
        let { id, user_name, password, email } = this.user;
        let data = {
          id,
          user_name,
          password,
          email,
        };
        putRequest('/user/update', data)
          .then(resp => {
            console.log(resp);
            if (resp.data.status === 200) {
              sessionStorage.setItem('user', JSON.stringify(this.user));
              this.$message({ type: 'success', message: '信息更新成功!' });
            }
          })
          .catch(err => {
            this.$message({ type: 'error', message: '信息更新失败!' });
          });
      },
    },
  };
</script>
