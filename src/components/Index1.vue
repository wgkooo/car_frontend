<template>
  <div class="wrapper">
    <el-row>
      <el-col :span="8" :offset="0">
        <br />
        <img src="../assets/images/head1.png" class="img1" />
      </el-col>
      <el-col :span="1" :offset="12">
        <img src="../assets/images/icon1.png" class="img2" />
      </el-col>
    </el-row>
    <br /><br />
    <el-row>
      <el-col :span="8" :offset="3">
        <el-button class="button1" @click="button1">
          <span>CUSTOMER SENTIMENT</span>
        </el-button>
      </el-col>
      <el-col :span="8" :offset="2">
        <el-button class="button2" @click="button2">
          <span>PRICING DEVELOPMENT</span>
        </el-button>
      </el-col>
    </el-row>
    <br /><br/>
    <el-row>
      <el-col :span="18" :offset="3">
        <el-button class="button3">
          <span>SALES TRENDS</span>
        </el-button>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  methods: {
    button1() {
      this.$router.push({ path: "/index2" });
    },
    button2() {
      this.$router.push({ path: "/pricingDevelopment" });
    },
  },
};
</script>
<style lang="less" scoped>
.wrapper {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.img1 {
  width: 100%;
}
.img2 {
  width: 300%;
}
.icon1 {
  position: absolute;
  top: 10px;
  left: 10px;
}
.icon2 {
  position: absolute;
  top: 10px;
  right: 30px;
}
.button1 {
//   height: 300px;
//   width: 600px;
  cursor: pointer;
  border-color: rgb(255, 255, 255);
  border: solid 1px rgb(2, 40, 120);
  width: 100%;
  padding-top: 25%;
  padding-bottom: 25%;
}
.button2 {
//   height: 300px;
//   width: 600px;
  cursor: pointer;
  border-color: rgb(255, 255, 255);
  border: solid 1px rgb(2, 40, 120);
  width: 100%;
  padding-top: 25%;
  padding-bottom: 25%;
}
span {
  color: rgb(2, 40, 120);
//   font-size: 20px;
  font-size: 140%;
}
.button3 {
//   height: 100px;
//   width: 1260px;
  cursor: pointer;
  border: solid 1px rgb(2, 40, 120);
  width: 100%;
  padding-top: 2%;
  padding-bottom: 2%;
}
</style>