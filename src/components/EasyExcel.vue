<template>
  <div class="wrapper">
    <br /><br />
    <el-row :gutter="20">
      <!-- 选择brand -->
      <el-col :span="4" :offset="2">
          <el-select v-model="brand" placeholder="select brand">
          <el-option
            v-for="item in brandOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value"
            
          >
          </el-option>
        </el-select>
      </el-col>

      <!-- 选择name -->
      <el-col :span="4">
        <el-select v-model="name" placeholder="select name">
          <el-option
            v-for="item in nameOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </el-col>

      <!-- 选择日期 -->
      <el-col :span="8">
        <el-date-picker
      v-model="searchDate"
      type="daterange"
      align="right"
      unlink-panels
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      :picker-options="pickerOptions">
    </el-date-picker>
      </el-col>
      <el-col :span="2">
        <el-button type="success" @click="search">search</el-button>
      </el-col>
      <el-col :span="2">
        <el-button type="success" @click="exportData">export</el-button>
      </el-col>
    </el-row>

    <el-row>
      <el-table :data="tableData" stripe style="width: 100%" v-show="tableShow">
        <el-table-column prop="brand" label="brand"></el-table-column>
        <el-table-column prop="model" label="model"></el-table-column>
        <el-table-column prop="name" label="name"> </el-table-column>

        <el-table-column prop="carseries" label="carseries"></el-table-column>
        <el-table-column prop="overall" label="overall"></el-table-column>
        <el-table-column prop="exterior" label="exterior"></el-table-column>
        <el-table-column prop="interior" label="interior"></el-table-column>
        <el-table-column prop="carspace" label="carspace"></el-table-column>
        <el-table-column prop="valueformoney" label="valueformoney"></el-table-column>
        <el-table-column prop="power" label="power"></el-table-column>
        <el-table-column prop="maneuverability" label="maneuverability"></el-table-column>
        <el-table-column prop="fuelconsumption" label="fuelconsumption"></el-table-column>
        <el-table-column prop="comfort" label="comfort"></el-table-column>
        <el-table-column prop="optionsandfeatures" label="optionsandfeatures"></el-table-column>
        <el-table-column prop="createdate" label="createdate"></el-table-column>
        <el-table-column prop="source" label="source"></el-table-column>
      </el-table>
    </el-row>

    <el-row>
      <el-pagination
      v-show="pageListShow"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page.sync="currentPage"
      :page-sizes="[5, 10, 15, 20]"
      :page-size="100"
      layout="sizes, prev, pager, next"
      :total="pageTotal">
    </el-pagination>
    </el-row>
  </div>
</template>
<script>
import fileDownload from "js-file-download";

export default {
  data() {
    return {
      brandOptions:'',
      brand: "",
      nameOptions: [{}],
      name: "",
      pickerOptions: {
        shortcuts: [
          {
            text: "最近一周",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit("pick", [start, end]);
            },
          },
          {
            text: "最近三个月",
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit("pick", [start, end]);
            },
          },
        ],
      },
      searchDate: "",
      tableData: [{}],
      currentPage: 0,
      dataNum: 5,
      pageListShow:false,
      tableShow:false,
      pageTotal:0,
    };
  },
  watch: {
    brand(newvalue, old) {
      this.queryAllNameByBrand();
    },
  },
  created() {
    this.queryAllBrand()
  },
  methods: {
    // 分页的函数：监听每页展示的数据
    handleSizeChange(val) {
      this.dataNum = val
      this.queryDataLimit()
      },
    // 分页的函数：监听当前是第几页
      handleCurrentChange(val) {
        this.currentPage = val
        this.queryDataLimit()
      },
    //begin
    queryAllNameByBrand() {
      this.axios({
        url: "/api/easyExcel/queryAllNameByBrand",
        method: "GET",
        params: {
          brand: this.brand,
        },
      }).then((resp) => {
        this.name = "";
        this.nameOptions = [];
        for (let index = 0; index < resp.data.result.length; index++) {
          this.nameOptions[index] = {
            label: resp.data.result[index].name,
            value: resp.data.result[index].name,
          };
        }
      });
    },
    // begin
    queryAllBrand() {
     this.axios({
        url: "/api/easyExcel/queryAllBrand",
        methods: "POST",
      }).then((resp) => {
        this.brandOptions = []
        for (let index = 0; index < resp.data.result.length; index++) {
          // this.brandOptions[index] = {
          //   label: resp.data[index].brand,
          //   value: resp.data[index].brand,
          // };
          // 事实上Vue只能使用push、pop、sort等数组方法，才能响应式更新视图
          this.brandOptions.push({
          label: resp.data.result[index].brand,
          value: resp.data.result[index].brand,
          }
          )
        }
      });
    },
    // begin
    search() {
      this.pageListShow = false
      this.tableShow = false
      this.pageTotal = 0
      this.queryDataLimit()
      this.queryByKoubeiLimitAllNum()
    },
    // begin
    exportData() {
      this.axios({
        url: "/api/easyExcel/exportExcel",
        method: "GET",
        responseType: "arraybuffer",
        headers: {
          "Content-Type": "application/json;charset=utf-8",
          accessToken: "niceyoo",
        },
        params: {
          brand: this.brand,
          name: this.name,
          beginDate: this.searchDate[0].toISOString().substr(0, 10),
          endDate: this.searchDate[1].toISOString().substr(0, 10),
        },
      }).then((resp) => {
          fileDownload(resp.data, "koubeiData.xlsx");
        })
    },
    // begin  分页查询
    queryDataLimit(){
      this.axios({
        url: "/api/easyExcel/queryByKoubeiLimitQuery",
        method: "GET",
        params: {
          brand: this.brand,
          name: this.name,
          beginDate: this.searchDate[0].toISOString().substr(0, 10),
          endDate: this.searchDate[1].toISOString().substr(0, 10),
          pagenumber: this.currentPage * this.dataNum,
          contentnum: this.dataNum,
        },
      }).then((resp) => {
        this.tableData = []
          for (let index = 0; index < resp.data.result.length; index++) {
            this.tableData[index] = {
              brand:resp.data.result[index].brand,
              model:resp.data.result[index].model,
              name:resp.data.result[index].name,
              carseries:resp.data.result[index].carseries,
              overall:resp.data.result[index].overall,
              exterior:resp.data.result[index].exterior,
              interior:resp.data.result[index].interior,
              carspace:resp.data.result[index].carspace,
              valueformoney:resp.data.result[index].valueformoney,
              power:resp.data.result[index].power,
              maneuverability:resp.data.result[index].maneuverability,
              fuelconsumption:resp.data.result[index].fuelconsumption,
              comfort:resp.data.result[index].comfort,
              optionsandfeatures:resp.data.result[index].optionsandfeatures,
              createdate:resp.data.result[index].createdate,
              source:resp.data.result[index].source,
            }
          }
          this.pageListShow = true
          this.tableShow = true
        })
    },

    // begin 分页查询的总条数
    queryByKoubeiLimitAllNum(){
      this.axios({
        url: "/api/easyExcel/queryByKoubeiLimitAllNum",
        methods: "GET",
        params: {
          brand: this.brand,
          name: this.name,
          beginDate: this.searchDate[0].toISOString().substr(0, 10),
          endDate: this.searchDate[1].toISOString().substr(0, 10),
          pagenumber: this.currentPage * this.dataNum,
          contentnum: this.dataNum,
        },
      }).then((resp) => {
        this.pageTotal = resp.data.result
        })
    },

    // begin
    test1() {
    },
    test2() {
      this.tableData = [];
      this.tableData[0] = {
        date: "111",
        name: "222",
        address: "333 1518 弄",
      };
    },
    //
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