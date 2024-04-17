<template>
  <div class="wrapper">
        <h1>情感正负性测试</h1>
      <br><br><br><br>

    <el-row :gutter="20">
        <el-col :span="4" :offset="9">
            <el-input v-model="text" placeholder="请输入内容"></el-input>
        </el-col>
        <el-col :span="2">
        <el-button type="success" @click="test1">测试</el-button>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import fileDownload from "js-file-download";

export default {
  data() {
    return {
        text:''
    };
  },
  methods: {
    // begin
    test1() {
        this.axios({
        url: "/api/textNNControl/emotion",
        method: "GET",
        params: {
          text: this.text,
        },
      }).then((resp) => {
          alert(resp.data[0])
        })
    },
  },
};
</script>
<style lang="less" scoped>
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
.el-col {
  border-radius: 4px;
}
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}
.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
</style>