<template>
  <div class="wrapper">
    <el-row>
      <el-col :span="1" :offset="20">
        <img src="../assets/images/icon1.png" class="img1" />
      </el-col>
    </el-row>
    <br /><br /><br /><br /><br /><br />

    <el-row>
      <el-col :span="1" :offset="4">
        <img src="../assets/images/icon2.png" class="img2" />
      </el-col>
    </el-row>

    <el-row>
      <el-col :span="1" :offset="7">
          <div class="login">
              <div class="email_one">E-Mail</div>
              <div class="email_two">password</div>
              <el-input v-model="username" class="username"></el-input>
              <el-input v-model="password" type="password" class="password"></el-input>
          </div>
      </el-col>
      <el-col :span="1" :offset="6">
        <el-button @click="login">
          <span>Enter</span>
        </el-button>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
   
    login() {
      this.axios({
        url: "/api/user/userLogin",
        method: "post",
        // params: {
        //   username: this.username,
        //   password: this.password,
        // },
        // 使用data，发送的是json格式的数据，不适用params
        data: { 
          username: this.username,
          password: this.password,
        },
      })
        .then((resp) => {
          this.$router.push({ path: "/index1" });
        })
        .catch((error) => {
          alert("账号或密码错误，请重新登陆");
          this.username = "";
          this.password = "";
        });
    },
  },
};
</script>
<style lang="less" scoped>
.login_container {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.img1 {
  width: 200px;
}
.img2 {
  width: 1000px;
}
.icon1 {
  position: absolute;
  top: 10px;
  right: 30px;
}
.icon2 {
  position: absolute;
  top: 250px;
  left: 200px;
}
.login {
//   position: absolute;
//   top: 420px;
//   left: 510px;
  width: 410px;
  height: 100px;
  border: solid 1px rgb(2, 40, 120);
}
.email {
  position: absolute;
  height: 35px;
  width: 400px;
  top: 10px;
  left: 20px;
}
.email_one {
  background-color: rgb(2, 40, 120);
//   float: left;
  position: relative;
  top: 10px;
  left: 10px;
  width: 130px;
  height: 35px;
  color: rgb(255, 255, 255);
  text-align: center;
  line-height: 35px;
}
.email_two{
  background-color: rgb(2, 40, 120);
//   float: left;
  position: relative;
  top: 20px;
  left: 10px;
  width: 130px;
  height: 35px;
  color: rgb(255, 255, 255);
  text-align: center;
  line-height: 35px;
}
.username{
    position: relative;
    top: -60px;
    left: 170px;
}
.password {
  position: relative;
  top: -15px;
  left: -35px;
}
.el-input {
  width: 50%;
}
/deep/.el-input__inner {
  border-radius: 0px;
  height: 35px;
  border: 1px solid rgb(2, 40, 120);
}
.el-button {
//   position: absolute;
//   top: 420px;
//   left: 950px;
  height: 100px;
  width: 170px;
  font-size: 30px;
  color: rgb(2, 40, 120);
  border: 1px solid rgb(2, 40, 120);
}
</style>