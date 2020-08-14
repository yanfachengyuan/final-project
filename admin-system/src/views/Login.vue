<template>
  <div class="login">
    <div class="login_box">
      <div class="avator">
        <img src="../assets/logo.png" alt />
      </div>
      <div class="login_form">
        <el-form ref="form" :model="form">
          <el-form-item class="info">
            <el-input v-model="form.username" prefix-icon="el-icon-user"></el-input>
          </el-form-item>
          <el-form-item class="info">
            <el-input v-model="form.password" prefix-icon="el-icon-lock"></el-input>
          </el-form-item>
          <el-form-item class="btns">
            <el-button type="primary" @click="onSubmit">登陆</el-button>
            <el-button>重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    onSubmit() {
      this.$axios.post('http://127.0.0.1:8888/api/private/v1/login',this.form).then(res=>{
          console.log(res.data)
      })
      this.$message({
          message: '恭喜你，这是一条成功消息',
          type: 'success'
        });
      console.log(this.form)
    },
  },
};
</script>

<style lang="less" scoped>
.login {
  background-color: #2b4b6b;
  height: 100%;

  .login_box {
    width: 450px;
    height: 300px;
    background-color: #ffffff;
    border-radius: 6px;
    position: absolute;
    top: calc(50% - 150px);
    left: calc(50% - 225px);
    .avator {
      width: 130px;
      height: 130px;
      border-radius: 50%;
      padding: 20px;
      margin: -75px auto;
      background-color: #ffffff;
      img {
        border-radius: 50%;
        background-color: #eee;
        width: 100%;
        height: 100%;
      }
    }
    .login_form {
      width: 100%;
      padding: 80px 0 0 0;
    }
  }
}
.btns{
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
}
.info{
    width: 80%;
    margin: 10px auto;
}
</style>