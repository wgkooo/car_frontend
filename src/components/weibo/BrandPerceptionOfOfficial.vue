<template>
  <div class="wrapper">
    <el-row>
      <el-col :span="4" :offset="19">
        <el-select v-model="value" placeholder="请选择" @change="selectChange">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </el-col>
    </el-row> 
    <el-row :gutter="20">
      <el-col :span="11">
        <el-table
          :data="tableDataUser"
          :key="itemkey"
          style="width: 100%"
          border
        >
          <el-table-column prop="id" label="序号"></el-table-column>
          <el-table-column prop="brand" label="品牌"></el-table-column>
          <el-table-column prop="following" label="关注"></el-table-column>
          <el-table-column prop="followed" label="粉丝"></el-table-column>
          <el-table-column prop="forum" label="帖子"></el-table-column>
          <el-table-column prop="time" label="爬取时间"></el-table-column>
          <!-- <el-table-column fixed="right" label="操作">
            <template slot-scope="scope">
              <el-button
                @click="handleClickUser(scope.row.id)"
                type="text"
                size="small"
                >刷新</el-button
              >
            </template>
          </el-table-column> -->
        </el-table>
      </el-col>
      <el-col :span="12">
        <el-table
          :data="officialpostData"
          :span-method="objectSpanMethod"
          border
          style="width: 100%"
          max-height="261"
          >>
          <el-table-column prop="brand" label="品牌"></el-table-column>
          <el-table-column
            prop="text"
            label="内容"
            width="200px"
          ></el-table-column>
          <el-table-column
            prop="commentscount"
            label="讨论数"
            width="60px"
          ></el-table-column>
          <el-table-column prop="timestring" label="时间"></el-table-column>
          <el-table-column prop="linkurl" label="链接" width="60px">
            <template slot-scope="scope">
              <el-link
                :href="scope.row.linkurl"
                target="_blank"
                class="buttonText"
                type="primary"
                :underline="false"
                >链接</el-link
              >
            </template>
          </el-table-column>
          <el-table-column prop="keywordsTimes" label="keyword出现次数"></el-table-column>
          <el-table-column prop="emotion" label="情感"></el-table-column>
        </el-table>
      </el-col>
    </el-row>

    <el-row :gutter="20">
      <el-col :span="6">
        <div class="cloud-wrap">
          <div class="cloud-box" ref="cloudEl" />
        </div>
      </el-col>

      <el-col :span="6" :offset="1">
        <div class="cloud-wrap">
          <div class="cloud-box" ref="cloudEl2" />
        </div>
      </el-col>

      <el-col :span="6" :offset="1">
        <div class="cloud-wrap">
          <div class="cloud-box" ref="cloudEl3" />
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import echarts from "echarts";
import wordcloud from "echarts-wordcloud";

export default {
  data() {
    return {
      options: [],
      value: "",
      selectBrandData: [],
      selectCompetitorsData: [],

      tableDataUser: [],
      itemkey: 0,
      officialpostData: [],

      wordcloud: wordcloud,
      cloudData: [],
      brand1: "",
      brand2: "",
      brand3: "",
    };
  },
  mounted() {
    // this.drawCloud(this.$refs.cloudEl,this.brand1);
    // this.drawCloud(this.$refs.cloudEl2,this.brand2);
    // this.drawCloud(this.$refs.cloudEl3,this.brand3);
    this.drawCloud(this.$refs.cloudEl, this.selectBrandData.toString());
    this.drawCloud(this.$refs.cloudEl2, this.selectCompetitorsData[0]);
    this.drawCloud(this.$refs.cloudEl3, this.selectCompetitorsData[1]);
  },
  created() {
    //  this.brand1 = "特斯拉"
    //  this.brand2 = "宝马"
    //  this.brand3 = "蔚来"
    this.selectBrandData = this.$route.query.selectBrandData;
    this.selectCompetitorsData = this.$route.query.selectCompetitorsData;

    this.getUserDatas1(this.selectBrandData.toString());
    this.getUserDatas2(this.selectCompetitorsData[0]);
    this.getUserDatas3(this.selectCompetitorsData[1]);

    // 获取所有车型官方微博的前三个帖子
    this.getofficialpostData();
    this.getDate();
  },
  methods: {
    async drawCloud(wrapEl, brand, date) {
      await this.axios({
        url: "/api/officialPost/wordcloud",
        method: "POST",
        params: {
          brand: brand,
          dates: date,
        },
      }).then((resp) => {
        this.cloudData = [];
        for (let i = 0; i < resp.data.length; i++) {
          this.cloudData[i] = {
            value: resp.data[i].value,
            name: resp.data[i].name,
          };
        }
      });

      let myChart = echarts.init(wrapEl);
      var option = {
        tooltip: {
          show: true,
        },
        series: [
          {
            name: "热词",
            type: "wordCloud",
            sizeRange: [12, 30],
            rotationRange: [-20, 20],
            shape: "circle",
            left: "center",
            top: "center",
            width: "100%",
            height: "80%",
            gridSize: 3,
            textPadding: 0,
            autoSize: {
              enable: true,
              minSize: 6,
            },
            textStyle: {
              normal: {
                color: function () {
                  return (
                    "rgb(" +
                    [
                      Math.round(Math.random() * 250),
                      Math.round(Math.random() * 250),
                      Math.round(Math.random() * 250),
                    ].join(",") +
                    ")"
                  );
                },
              },
              emphasis: {
                shadowBlur: 10,
                shadowColor: "#333",
              },
            },
            data: this.cloudData,
          },
        ],
      };
      myChart.setOption(option);
    },
    objectSpanMethod({ row, column, rowIndex, columnIndex }) {
      if (columnIndex === 0) {
        if (rowIndex % 3 === 0) {
          return {
            rowspan: 3,
            colspan: 1,
          };
        } else {
          return {
            rowspan: 0,
            colspan: 0,
          };
        }
      }
    },
    handleClickUser(row) {
      if (row == 1) {
        this.getUserDatas1(this.selectBrandData.toString());
      } else if (row == 2) {
        this.getUserDatas2(this.selectCompetitorsData[0]);
      } else if (row == 3) {
        this.getUserDatas3(this.selectCompetitorsData[1]);
      }
    },
    async getUserDatas1(carbrand, date) {
      await this.axios({
        url: "/api/officialPost/getOfficialWeiBo",
        method: "POST",
        params: {
          brand: carbrand,
          dates: date,
        },
      }).then((resp) => {
        this.itemkey = Math.random();
        this.tableDataUser[0] = {
          id: 1,
          brand: resp.data["brand"],
          following: resp.data["followingnum"],
          followed: resp.data["followednum"],
          forum: resp.data["forumnum"],
          time: resp.data["timestring"],
        };
      });
    },
    async getUserDatas2(carbrand, date) {
      await this.axios({
        url: "/api/officialPost/getOfficialWeiBo",
        method: "POST",
        params: {
          brand: carbrand,
          dates: date,
        },
      }).then((resp) => {
        this.itemkey = Math.random();
        this.tableDataUser[1] = {
          id: 2,
          brand: resp.data["brand"],
          following: resp.data["followingnum"],
          followed: resp.data["followednum"],
          forum: resp.data["forumnum"],
          time: resp.data["timestring"],
        };
      });
    },
    async getUserDatas3(carbrand, date) {
      await this.axios({
        url: "/api/officialPost/getOfficialWeiBo",
        method: "POST",
        params: {
          brand: carbrand,
          dates: date,
        },
      }).then((resp) => {
        this.itemkey = Math.random();
        this.tableDataUser[2] = {
          id: 3,
          brand: resp.data["brand"],
          following: resp.data["followingnum"],
          followed: resp.data["followednum"],
          forum: resp.data["forumnum"],
          time: resp.data["timestring"],
        };
      });
    },
    getDate() {
      this.axios({
        url: "/api/officialPost/getDate",
        method: "POST",
      }).then((resp) => {
        // 设置date列表
        let datalength = resp.data.length;
        for (let index = 0; index < datalength; index++) {
          this.options.push({
            value: resp.data[index],
            label: resp.data[index],
          });
        }
        //设置默认date
        // this.value = resp.data[datalength - 1];
        this.value = resp.data[0];
      });
    },
    getofficialpostData(date) {
      this.axios({
        url: "/api/officialPost/selectAllByTime",
        method: "POST",
        params: {
          dates: date,
        },
      }).then((resp) => {
        this.officialpostData = resp.data;
      });
    },
    selectChange() {
      this.drawCloud(
        this.$refs.cloudEl,
        this.selectBrandData.toString(),
        this.value
      );
      this.drawCloud(
        this.$refs.cloudEl2,
        this.selectCompetitorsData[0],
        this.value
      );
      this.drawCloud(
        this.$refs.cloudEl3,
        this.selectCompetitorsData[1],
        this.value
      );

      this.getofficialpostData(this.value);

      if (this.selectBrandData[0] != ''){
        this.getUserDatas1(this.selectBrandData[0], this.value)
      }
      if (this.selectCompetitorsData[0] != '') {
        this.getUserDatas2(this.selectCompetitorsData[0], this.value)
      }
      if (this.selectCompetitorsData[1] != undefined) {
        this.getUserDatas3(this.selectCompetitorsData[1], this.value)
      }
    },
  },
};
</script>
<style lang="less" scoped>
.wrapper {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.chartsClass {
  padding-left: 1.2rem;
}
.cloud-wrap {
  width: 490px;
  height: 366px;
  text-align: left;
  .cloud-box {
    width: 100%;
    height: 100%;
  }
}
</style>