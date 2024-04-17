<template>
  <div class="wrapper">
    <br><br><br><br><br><br>
    <el-row>
      <el-col :span="6" :offset="2">
        <el-button @click="button1">
          <span>PRODUCT</span>
          <span>EVALUATION</span>
        </el-button>
      </el-col>
      <el-col :span="6" :offset="1">
        <el-button @click="button2">
          <span>RETAIL</span>
          <span>EXPERIENCE</span>
        </el-button>
      </el-col>
      <el-col :span="6" :offset="1">
        <el-button @click="button3">
          <span>BRAND</span>
          <span>PERCEPTION</span>
        </el-button>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  methods: {
    button1() {
      this.$router.push({ path: "/productEvaluation" });
    },
    button2() {
      this.$router.push({ path: "/retailExperience" });
    },
    button3() {
      this.$router.push({ path: "/brandPerception" });
    },
  },
};
</script>
<style lang="less" scoped>
.wrapper {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.el-button {
  height: 400px;
  width: 300px;
  border: 1px solid rgb(2, 40, 120);
}
span {
  color: rgb(2, 40, 120);
  font-size: 20px;
  display: block;
  margin-top: 8px;
}
</style>