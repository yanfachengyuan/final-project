<template>
  <div class="login">
    <div class="login_box">
      <div class="avator">
        <img src="../assets/logo.png" alt />
      </div>
      <div class="login_form">
        <el-form ref="form" :model="form" :rules="loginRules">
          <el-form-item class="info" prop="loginName">
            <el-input v-model="form.username" prefix-icon="el-icon-user"></el-input>
          </el-form-item>
          <el-form-item class="info" prop="loginPsd">
            <el-input v-model="form.password" prefix-icon="el-icon-lock" type="password"></el-input>
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
        username: "admin",
        password: "123456",
      },
      loginRules: {
        loginName: [
          { required: true, message: "请输入用户名", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        loginPsd: [
          { required: true, message: "请输入密码", trigger: "blur" },
          {
            min: 6,
            max: 10,
            message: "长度在 6 到 10 个字符",
            trigger: "blur",
          },
        ],
      },
    };
  },
  methods: {
    async onSubmit() {
      let { data } = await this.$axios.post("login", this.form);
      window.sessionStorage.setItem("token", data.data.token);
      this.$message({
        message: data.meta.message,
        type: "success",
      });
      this.$router.push("/home");
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
      padding: 60px 0 0 0;
    }
  }
}
.btns {
  display: flex;
  justify-content: space-around;
  margin-top: 30px;
}
.info {
  width: 80%;
  margin: 20px auto;
}
</style>