<template>
  <div class="wrapper">
    <div class="select">
      <el-button class="select1" @click="btn1">
        <span>Vehicle ratings</span>
      </el-button>
      <el-button class="select2" @click="btn2">
        <span>Forum discussions</span>
      </el-button>
    </div>
    <div class="koubieHeaders" v-show="koubeiHeaders">
      <div class="header2">
        <span class="headerSpan">Total posts analysed</span>
      </div>
      <div class="header4">
        <span class="headerSpan">{{ koubeiNum }}</span>
      </div>
    </div>
    <div class="headers" v-show="headers">
      <div class="header1"><span class="headerSpan">Timeframe</span></div>
      <div class="header2">
        <span class="headerSpan">Total posts analysed</span>
      </div>
      <div class="header3"><span class="headerSpan">Q2/2020</span></div>
      <div class="header4"><span class="headerSpan">25,200</span></div>
    </div>
    <div class="show1" v-show="show1">
      <span class="title">VEHICLE RATING</span>
      <span class="brand1">{{ brand1Datas.brand }}</span>
      <span class="brand2">{{ brand2Datas.brand }}</span>
      <span class="brand3">{{ brand3Datas.brand }}</span>
      <span class="brand4">{{ brand4Datas.brand }}</span>
      <span class="brand5">{{ brand5Datas.brand }}</span>

      <div id="barChart1" class="BarChart1" v-show="barChar1Show"></div>
      <div id="barChart2" class="BarChart2" v-show="barChar2Show"></div>
      <div id="barChart3" class="BarChart3" v-show="barChar3Show"></div>
      <div id="barChart4" class="BarChart4" v-show="barChar4Show"></div>
      <div id="barChart5" class="BarChart5" v-show="barChar5Show"></div>

      <el-select
        v-model="value"
        placeholder="请选择"
        @change="selectChange"
        size="mini"
      >
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>

      <div class="footer">
        <div class="footer1">PEER COMPARISON</div>
        <div class="footer2">Key strengths</div>
        <div class="footer3">{{ brand1Datas.strengths }}</div>
        <div class="footer4">Key weaknesses</div>
        <div class="footer5">{{ brand1Datas.weaknesses }}</div>
      </div>
    </div>
  </div>
</template>
<script>
import Echarts from "echarts";
export default {
  data() {
    return {
      options: [
        //        {
        //     value: '2020-09',
        //     label: '2020-09'
        //   }, {
        //     value: '2020-08',
        //     label: '2020-08'
        //   },{
        //     value: '2020-07',
        //     label: '2020-07'
        //   },
        //   {
        //     value: '2020-06',
        //     label: '2020-06'
        //   },
        {},
      ],
      value: "",
      list1style: "",
      list2style: "",
      list3style: "",
      list4style: "",
      list5style: "",
      koubeiHeaders: true,
      brand1Num: 0,
      brand2Num: 0,
      brand3Num: 0,
      brand4Num: 0,
      brand5Num: 0,
      koubeiNum: 0,

      overallColor1: "",
      exteriorColor1: "",
      interiorColor1: "",
      carspaceColor1: "",
      valueformoneyColor1: "",
      powerColor1: "",
      maneuverabilityColor1: "",
      fuelconsumptionColor1: "",
      comfortColor1: "",
      optionsandfeaturesColor1: "",

      overallColor2: "",
      exteriorColor2: "",
      interiorColor2: "",
      carspaceColor2: "",
      valueformoneyColor2: "",
      powerColor2: "",
      maneuverabilityColor2: "",
      fuelconsumptionColor2: "",
      comfortColor2: "",
      optionsandfeaturesColor2: "",

      overallColor3: "",
      exteriorColor3: "",
      interiorColor3: "",
      carspaceColor3: "",
      valueformoneyColor3: "",
      powerColor3: "",
      maneuverabilityColor3: "",
      fuelconsumptionColor3: "",
      comfortColor3: "",
      optionsandfeaturesColor3: "",

      overallColor4: "",
      exteriorColor4: "",
      interiorColor4: "",
      carspaceColor4: "",
      valueformoneyColor4: "",
      powerColor4: "",
      maneuverabilityColor4: "",
      fuelconsumptionColor4: "",
      comfortColor4: "",
      optionsandfeaturesColor4: "",

      overallColor5: "",
      exteriorColor5: "",
      interiorColor5: "",
      carspaceColor5: "",
      valueformoneyColor5: "",
      powerColor5: "",
      maneuverabilityColor5: "",
      fuelconsumptionColor5: "",
      comfortColor5: "",
      optionsandfeaturesColor5: "",

      brand1datasShow: true,
      brand2datasShow: true,
      brand3datasShow: true,
      brand4datasShow: true,
      brand5datasShow: true,

      show1: true,
      show2: false,
      
      headers: false,
      select1: "",
      select2: [],
      select3: [],
      brand1Datas: {
        overall: 0,
        exterior: 0,
        interior: 0,
        carspace: 0,
        valueformoney: 0,
        power: 0,
        maneuverability: 0,
        fuelconsumption: 0,
        comfort: 0,
        optionsandfeatures: 0,
      },
      brand2Datas: {
        overall: 0,
        exterior: 0,
        interior: 0,
        carspace: 0,
        valueformoney: 0,
        power: 0,
        maneuverability: 0,
        fuelconsumption: 0,
        comfort: 0,
        optionsandfeatures: 0,
      },
      brand3Datas: {
        overall: 0,
        exterior: 0,
        interior: 0,
        carspace: 0,
        valueformoney: 0,
        power: 0,
        maneuverability: 0,
        fuelconsumption: 0,
        comfort: 0,
        optionsandfeatures: 0,
      },
      brand4Datas: {
        overall: 0,
        exterior: 0,
        interior: 0,
        carspace: 0,
        valueformoney: 0,
        power: 0,
        maneuverability: 0,
        fuelconsumption: 0,
        comfort: 0,
        optionsandfeatures: 0,
      },
      brand5Datas: {
        overall: 0,
        exterior: 0,
        interior: 0,
        carspace: 0,
        valueformoney: 0,
        power: 0,
        maneuverability: 0,
        fuelconsumption: 0,
        comfort: 0,
        optionsandfeatures: 0,
      },
      pieCharts: null,
      pieCharts1: null,
      pieCharts2: null,

      barCharts1: null,
      barCharts2: null,
      barCharts3: null,
      barCharts4: null,
      barCharts5: null,
      barChar1Show: false,
      barChar2Show: false,
      barChar3Show: false,
      barChar4Show: false,
      barChar5Show: false,
      barOption1: {
        grid: {
          width: "10%",
          left: "6%",
        },
        xAxis: {
          max: 1,
          axisLabel: {
            show: false, // 不显示横坐标的值
          },
          splitLine: {
            show: false,
          },
          axisLine: { 
             show: false,
             }, //不显示坐标轴
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        yAxis: {
          type: "category",
          data: [
            "Optionsandfeatures",
            "Comfort",
            "Fuelconsumption",
            "Maneuverability",
            "Power",
            "Valueformoney",
            "CarSpace",
            "Interior",
            "Exterior",
            "Overall",
          ],
          axisLabel: {
            interval: "auto",
            show: true, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 12,
          },
          axisLine: { 
             show: true,
             },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          {
            // name: "X",
            type: "bar",
            // barWidth: 20,
            data: [
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
            ],
            label: {
              show: true,
              position: "right",
              valueAnimation: true,
            },
          },
        ],
        legend: {
          show: true,
        },
      },
      barOption2: {
        grid: {
          width: "10%",
          // left: "6%",
        },
        xAxis: {
          max: 1,
          axisLabel: {
            show: false, // 不显示横坐标的值
          },
          splitLine: {
            show: false,
          },
          axisLine: { show: false }, //不显示坐标轴
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        yAxis: {
          type: "category",
          data: [
            "Optionsandfeatures",
            "Comfort",
            "Fuelconsumption",
            "Maneuverability",
            "Power",
            "Valueformoney",
            "CarSpace",
            "Interior",
            "Exterior",
            "Overall",
          ],
          axisLabel: {
            interval: "auto",
            show: false, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 13,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          {
            type: "bar",
            stack: 2,
            data: [
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
            ],
            label: {
              show: true,
              position: "right",
              valueAnimation: true,
            },
          },
        ],
        legend: {
          show: true,
        },
      },
      barOption3: {
        grid: {
          width: "10%",
          // left: "7%",
        },
        xAxis: {
          max: 1,
          axisLabel: {
            show: false, // 不显示横坐标的值
          },
          splitLine: {
            show: false,
          },
          axisLine: { show: false }, //不显示坐标轴
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        yAxis: {
          type: "category",
          data: [
            "Optionsandfeatures",
            "Comfort",
            "Fuelconsumption",
            "Maneuverability",
            "Power",
            "Valueformoney",
            "CarSpace",
            "Interior",
            "Exterior",
            "Overall",
          ],
          axisLabel: {
            interval: "auto",
            show: false, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 13,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          {
            // name: "X",
            type: "bar",
            data: [
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
            ],
            label: {
              show: true,
              position: "right",
              valueAnimation: true,
            },
          },
        ],
        legend: {
          show: true,
        },
      },
      barOption4: {
        grid: {
          width: "10%",
          // left: "7%",
        },
        xAxis: {
          max: 1,
          axisLabel: {
            show: false, // 不显示横坐标的值
          },
          splitLine: {
            show: false,
          },
          axisLine: { show: false }, //不显示坐标轴
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        yAxis: {
          type: "category",
          data: [
            "Optionsandfeatures",
            "Comfort",
            "Fuelconsumption",
            "Maneuverability",
            "Power",
            "Valueformoney",
            "CarSpace",
            "Interior",
            "Exterior",
            "Overall",
          ],
          axisLabel: {
            interval: "auto",
            show: false, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 13,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          {
            // name: "X",
            type: "bar",
            data: [
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
            ],
            label: {
              show: true,
              position: "right",
              valueAnimation: true,
            },
          },
        ],
        legend: {
          show: true,
        },
      },
      barOption5: {
        grid: {
          width: "10%",
          // left: "7%",
        },
        xAxis: {
          max: 1,
          axisLabel: {
            show: false, // 不显示横坐标的值
          },
          splitLine: {
            show: false,
          },
          axisLine: { show: false }, //不显示坐标轴
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        yAxis: {
          type: "category",
          data: [
            "Optionsandfeatures",
            "Comfort",
            "Fuelconsumption",
            "Maneuverability",
            "Power",
            "Valueformoney",
            "CarSpace",
            "Interior",
            "Exterior",
            "Overall",
          ],
          axisLabel: {
            interval: "auto",
            show: false, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 13,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          {
            // name: "X",
            type: "bar",
            data: [
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
              { value: 0, itemStyle: { color: "#849fca" } },
            ],
            label: {
              show: true,
              position: "right",
              valueAnimation: true,
            },
          },
        ],
        legend: {
          show: true,
        },
      },
    };
  },
  created() {
    this.select1 = this.$route.select1;
    this.select2 = this.$route.query.select2[0];
    this.select3 = this.$route.query.select3;

    this.getBrand1Datas();
    this.getBrand2Datas();
    this.getBrand3Datas();
    this.getBrand4Datas();
    this.getBrand5Datas();

    this.getdata();
  },
  mounted() {
    this.$nextTick(() => {
      // 这里初始化，然后再getbrand函数中设置
      this.barCharts1 = Echarts.init(document.getElementById("barChart1"));
      // this.barCharts1.setOption(this.barOption1);

      this.barCharts2 = Echarts.init(document.getElementById("barChart2"));
      // this.barCharts2.setOption(this.barOption2);

      this.barCharts3 = Echarts.init(document.getElementById("barChart3"));
      // this.barCharts3.setOption(this.barOption3);

      this.barCharts4 = Echarts.init(document.getElementById("barChart4"));
      // this.barCharts4.setOption(this.barOption4);

      this.barCharts5 = Echarts.init(document.getElementById("barChart5"));
      // this.barCharts5.setOption(this.barOption5);
    });
  },
  watch: {
    value(newvalue, oldvalue) {
      this.$router.push({
        path: "/productEvaluationByCarBrand",
        query: {
          select1: this.select2,
          select2: this.select2,
          select3: this.select3,
        },
      });
    },
    brand1Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue;
    },
    brand2Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue;
    },
    brand3Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue;
    },
    brand4Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue;
    },
    brand5Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue;
    },
  },
  methods: {
    // 获取日期
    getdata() {
      this.axios({
        url: "/api/koubei/querydate",
        method: "GET",
      }).then((resp) => {
        let datalength = resp.data.dataSet.length;
        this.value = resp.data.dataSet[datalength - 1].substring(0, 7);
        this.options[0].value = resp.data.dataSet[datalength - 1];
        this.options[0].label = resp.data.dataSet[datalength - 1].substring(
          0,
          7
        );
        for (let index = datalength - 2; index >= 0; index--) {
          this.options.push({
            value: resp.data.dataSet[index],
            label: resp.data.dataSet[index].substring(0, 7),
          });
        }
      });
    },
    // 找到最大值
    findMax(param1, param2, param3, param4, param5) {
      let maxNum = param1;
      let maxBrand = "brand1";

      if (param2 > maxNum) {
        maxNum = param2;
        maxBrand = "brand2";
      }
      if (param3 > maxNum) {
        maxNum = param3;
        maxBrand = "brand3";
      }
      if (param4 > maxNum) {
        maxNum = param4;
        maxBrand = "brand4";
      }
      if (param5 > maxNum) {
        maxNum = param5;
        maxBrand = "brand5";
      }
      return maxBrand;
    },
    // 获取 brand 数据
    showBrand1Datas() {
      let brand;
      brand = this.findMax(
        this.brand1Datas.overall,
        this.brand2Datas.overall,
        this.brand3Datas.overall,
        this.brand4Datas.overall,
        this.brand5Datas.overall
      );
      // 找最大的overall
      if (brand == "brand1") {
        // 设置颜色
        this.barOption1.series[0].data[9].itemStyle.color = "orange";
        this.barOption2.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[9].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[9].itemStyle.color = "orange";
        this.barOption3.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[9].itemStyle.color = "#849fca";
        
        this.reLoadBar()
      } else if (brand == "brand3") {
        // 设置颜色
        // 设置颜色
        this.barOption1.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[9].itemStyle.color = "orange";
        this.barOption4.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[9].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        // 设置颜色
        this.barOption1.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[9].itemStyle.color = "orange";
        this.barOption5.series[0].data[9].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[9].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[9].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.exterior,
        this.brand2Datas.exterior,
        this.brand3Datas.exterior,
        this.brand4Datas.exterior,
        this.brand5Datas.exterior
      );
      if (brand == "brand1") {
         // 设置颜色
        this.barOption1.series[0].data[8].itemStyle.color = "orange";
        this.barOption2.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[8].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[8].itemStyle.color = "orange";
        this.barOption3.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[8].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        // 设置颜色
        this.barOption1.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[8].itemStyle.color = "orange";
        this.barOption4.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[8].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        // 设置颜色
        this.barOption1.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[8].itemStyle.color = "orange";
        this.barOption5.series[0].data[8].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[8].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[8].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.interior,
        this.brand2Datas.interior,
        this.brand3Datas.interior,
        this.brand4Datas.interior,
        this.brand5Datas.interior
      );
      if (brand == "brand1") {
        // 设置颜色
        this.barOption1.series[0].data[7].itemStyle.color = "orange";
        this.barOption2.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[7].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
         // 设置颜色
        this.barOption1.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[7].itemStyle.color = "orange";
        this.barOption3.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[7].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        // 设置颜色
        this.barOption1.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[7].itemStyle.color = "orange";
        this.barOption4.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[7].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
         // 设置颜色
        this.barOption1.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[7].itemStyle.color = "orange";
        this.barOption5.series[0].data[7].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[7].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[7].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.carspace,
        this.brand2Datas.carspace,
        this.brand3Datas.carspace,
        this.brand4Datas.carspace,
        this.brand5Datas.carspace
      );
      if (brand == "brand1") {
         // 设置颜色
        this.barOption1.series[0].data[6].itemStyle.color = "orange";
        this.barOption2.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[6].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
         // 设置颜色
        this.barOption1.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[6].itemStyle.color = "orange";
        this.barOption3.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[6].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
         // 设置颜色
        this.barOption1.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[6].itemStyle.color = "orange";
        this.barOption4.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[6].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
         // 设置颜色
        this.barOption1.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[6].itemStyle.color = "orange";
        this.barOption5.series[0].data[6].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
         // 设置颜色
        this.barOption1.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[6].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[6].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.valueformoney,
        this.brand2Datas.valueformoney,
        this.brand3Datas.valueformoney,
        this.brand4Datas.valueformoney,
        this.brand5Datas.valueformoney
      );
      if (brand == "brand1") {
         // 设置颜色
        this.barOption1.series[0].data[5].itemStyle.color = "orange";
        this.barOption2.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[5].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
         // 设置颜色
        this.barOption1.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[5].itemStyle.color = "orange";
        this.barOption3.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[5].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
         // 设置颜色
        this.barOption1.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[5].itemStyle.color = "orange";
        this.barOption4.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[5].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
         // 设置颜色
        this.barOption1.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[5].itemStyle.color = "orange";
        this.barOption5.series[0].data[5].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[5].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[5].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.power,
        this.brand2Datas.power,
        this.brand3Datas.power,
        this.brand4Datas.power,
        this.brand5Datas.power
      );
      if (brand == "brand1") {
         // 设置颜色
        this.barOption1.series[0].data[4].itemStyle.color = "orange";
        this.barOption2.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[4].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[4].itemStyle.color = "orange";
        this.barOption3.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[4].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        // 设置颜色
        this.barOption1.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[4].itemStyle.color = "orange";
        this.barOption4.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[4].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        // 设置颜色
        this.barOption1.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[4].itemStyle.color = "orange";
        this.barOption5.series[0].data[4].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[4].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[4].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.maneuverability,
        this.brand2Datas.maneuverability,
        this.brand3Datas.maneuverability,
        this.brand4Datas.maneuverability,
        this.brand5Datas.maneuverability
      );
      if (brand == "brand1") {
        // 设置颜色
        this.barOption1.series[0].data[3].itemStyle.color = "orange";
        this.barOption2.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[3].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[3].itemStyle.color = "orange";
        this.barOption3.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[3].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        // 设置颜色
        this.barOption1.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[3].itemStyle.color = "orange";
        this.barOption4.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[3].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        // 设置颜色
        this.barOption1.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[3].itemStyle.color = "orange";
        this.barOption5.series[0].data[3].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[3].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[3].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.fuelconsumption,
        this.brand2Datas.fuelconsumption,
        this.brand3Datas.fuelconsumption,
        this.brand4Datas.fuelconsumption,
        this.brand5Datas.fuelconsumption
      );
      if (brand == "brand1") {
        // 设置颜色
        this.barOption1.series[0].data[2].itemStyle.color = "orange";
        this.barOption2.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[2].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[2].itemStyle.color = "orange";
        this.barOption3.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[2].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
       // 设置颜色
        this.barOption1.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[2].itemStyle.color = "orange";
        this.barOption4.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[2].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        // 设置颜色
        this.barOption1.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[2].itemStyle.color = "orange";
        this.barOption5.series[0].data[2].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        // 设置颜色
        this.barOption1.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[2].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[2].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.comfort,
        this.brand2Datas.comfort,
        this.brand3Datas.comfort,
        this.brand4Datas.comfort,
        this.brand5Datas.comfort
      );
      if (brand == "brand1") {
        // 设置颜色
        this.barOption1.series[0].data[1].itemStyle.color = "orange";
        this.barOption2.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[1].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        // 设置颜色
        this.barOption1.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[1].itemStyle.color = "orange";
        this.barOption3.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[1].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        this.barOption1.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[1].itemStyle.color = "orange";
        this.barOption4.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[1].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        this.barOption1.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[1].itemStyle.color = "orange";
        this.barOption5.series[0].data[1].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        this.barOption1.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[1].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[1].itemStyle.color = "orange";

        this.reLoadBar()
      }
      brand = this.findMax(
        this.brand1Datas.optionsandfeatures,
        this.brand2Datas.optionsandfeatures,
        this.brand3Datas.optionsandfeatures,
        this.brand4Datas.optionsandfeatures,
        this.brand5Datas.optionsandfeatures
      );
      if (brand == "brand1") {
        this.barOption1.series[0].data[0].itemStyle.color = "orange";
        this.barOption2.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[0].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand2") {
        this.barOption1.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[0].itemStyle.color = "orange";
        this.barOption3.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[0].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand3") {
        this.barOption1.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[0].itemStyle.color = "orange";
        this.barOption4.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[0].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand4") {
        this.barOption1.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[0].itemStyle.color = "orange";
        this.barOption5.series[0].data[0].itemStyle.color = "#849fca";

        this.reLoadBar()
      } else if (brand == "brand5") {
        this.barOption1.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption2.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption3.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption4.series[0].data[0].itemStyle.color = "#849fca";
        this.barOption5.series[0].data[0].itemStyle.color = "orange";

        this.reLoadBar()
      }
    },
    getBrand1Datas() {
      if (this.select2 != "") {
        this.axios({
          url: "/api/koubei/selectAllByBrand",
          method: "POST",
          params: {
            brand: this.select2,
            date: this.value,
          },
        }).then((resp) => {
          this.brand1Datas = resp.data.result;

          this.barOption1.series[0].data = [];
          this.barOption1.series[0].data.push({
            value: resp.data.result.optionsandfeatures,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.comfort,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.fuelconsumption,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.maneuverability,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.power,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.valueformoney,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.carspace,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.interior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.exterior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption1.series[0].data.push({
            value: resp.data.result.overall,
            itemStyle: { color: "#849fca" },
          });

          this.showBrand1Datas();
          this.brand1Num = resp.data.result.datanum;

          this.barCharts1.setOption(this.barOption1);
          this.barChar1Show = true
        });
      }
    },
    // 当改变日期的时候，重新获取五个brand的数据
    selectChange() {
      this.getBrand1Datas();
      this.getBrand2Datas();
      this.getBrand3Datas();
      this.getBrand4Datas();
      this.getBrand5Datas();
    },
    getBrand2Datas() {
      if (this.select3.length >= 1) {
        this.axios({
          url: "/api/koubei/selectAllByBrand",
          method: "POST",
          params: { brand: this.select3[0], date: this.value },
        }).then((resp) => {
          this.brand2Datas = resp.data.result;

          this.barOption2.series[0].data = [];
          this.barOption2.series[0].data.push({
            value: resp.data.result.optionsandfeatures,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.comfort,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.fuelconsumption,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.maneuverability,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.power,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.valueformoney,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.carspace,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.interior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.exterior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption2.series[0].data.push({
            value: resp.data.result.overall,
            itemStyle: { color: "#849fca" },
          });

          this.showBrand1Datas();
          this.brand2Num = resp.data.result.datanum;

          // 更新柱状图
          this.barCharts2.setOption(this.barOption2);
          this.barChar2Show = true
        });
      } else {
        // 不显示这个柱状图
      }
    },
    getBrand3Datas() {
      if (this.select3.length >= 2) {
        this.axios({
          url: "/api/koubei/selectAllByBrand",
          method: "POST",
          params: { brand: this.select3[1], date: this.value },
        }).then((resp) => {
          this.brand3Datas = resp.data.result;

          this.barOption3.series[0].data = [];
          this.barOption3.series[0].data.push({
            value: resp.data.result.optionsandfeatures,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.comfort,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.fuelconsumption,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.maneuverability,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.power,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.valueformoney,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.carspace,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.interior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.exterior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption3.series[0].data.push({
            value: resp.data.result.overall,
            itemStyle: { color: "#849fca" },
          });

          this.showBrand1Datas();

          this.brand3Num = resp.data.result.datanum;

          // 更新柱状图
          this.barCharts3.setOption(this.barOption3);
          this.barChar3Show = true
        });
      }
    },
    getBrand4Datas() {
      if (this.select3.length >= 3) {
        this.axios({
          url: "/api/koubei/selectAllByBrand",
          method: "POST",
          params: { brand: this.select3[2], date: this.value },
        }).then((resp) => {
          this.brand4Datas = resp.data.result;

          this.barOption4.series[0].data = [];
          this.barOption4.series[0].data.push({
            value: resp.data.result.optionsandfeatures,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.comfort,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.fuelconsumption,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.maneuverability,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.power,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.valueformoney,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.carspace,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.interior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.exterior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption4.series[0].data.push({
            value: resp.data.result.overall,
            itemStyle: { color: "#849fca" },
          });

          this.showBrand1Datas();

          this.brand4Num = resp.data.result.datanum;

          // 更新柱状图
          this.barCharts4.setOption(this.barOption4);
          this.barChar4Show = true
        });
      } else {
        // 不显示这个柱状图
      }
    },
    getBrand5Datas() {
      if (this.select3.length >= 4) {
        this.axios({
          url: "/api/koubei/selectAllByBrand",
          method: "POST",
          params: { brand: this.select3[3], date: this.value },
        }).then((resp) => {
          this.brand5Datas = resp.data.result;

          this.barOption5.series[0].data = [];
          this.barOption5.series[0].data.push({
            value: resp.data.result.optionsandfeatures,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.comfort,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.fuelconsumption,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.maneuverability,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.power,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.valueformoney,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.carspace,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.interior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.exterior,
            itemStyle: { color: "#849fca" },
          });
          this.barOption5.series[0].data.push({
            value: resp.data.result.overall,
            itemStyle: { color: "#849fca" },
          });

          this.showBrand1Datas();

          this.brand5Num = resp.data.result.datanum;

          // 更新柱状图
          this.barCharts5.setOption(this.barOption5);
          this.barChar5Show = true
        });
      } else {
        // 不显示这个柱状图
      }
    },

    reLoadBar() {
      this.barCharts1.setOption(this.barOption1);
      this.barCharts2.setOption(this.barOption2);
      this.barCharts3.setOption(this.barOption3);
      this.barCharts4.setOption(this.barOption4);
      this.barCharts5.setOption(this.barOption5);
    },

    btn1() {},
    btn2() {},
  },
};
</script>
<style lang="less" scoped>
.select {
  position: absolute;
  top: 100px;
  left: 100px;
  width: 530px;
  height: 30px;
  border: 1px solid rgb(2, 40, 120);
  border-bottom: none;
}
.koubieHeaders {
  position: absolute;
  width: 369px;
  height: 15px;
  border: 1px solid rgb(81, 82, 84);
  border-bottom: none;
  border-left: none;
  top: 114px;
  left: 632px;
}
.select1 {
  position: absolute;
  top: 0px;
  left: 0px;
  width: 265px;
  height: 30px;
  border-radius: 0px;
}
.select2 {
  position: absolute;
  top: 0px;
  right: 0px;
  width: 265px;
  height: 30px;
  border-radius: 0px;
}
.show1 {
  position: absolute;
  top: 130px;
  left: 100px;
  width: 1271px;
  height: 460px;
  border: 1px solid rgb(2, 40, 120);
}
.show2 {
  position: absolute;
  top: 230px;
  left: 300px;
  width: 900px;
  height: 400px;
  border: 1px solid rgb(2, 40, 120);
}
.title {
  position: absolute;
  top: 10px;
  left: 10px;
  color: rgb(2, 40, 120);
  display: block;
}
.el-progress {
  padding-top: 10px;
  padding-left: 136px;
  width: 300px;
}
/deep/.el-progress-bar__outer {
  border-radius: 0px;
  background-color: rgb(255, 255, 255);
}
/deep/.el-progress-bar__inner {
  border-radius: 0px;
  background-color: rgb(132, 159, 202);
}
.progress1 {
  padding-top: 90px;
}
/deep/.el-progress-bar__innerText {
  color: rgb(132, 159, 202);
}
.el-divider {
  position: absolute;
  top: 79px;
  left: 127px;
  height: 16em;
  background-color: black;
}
.list {
  position: absolute;
  top: 81px;
  left: 2px;
}
.spanList {
  display: block;
  padding-top: 13px;
  font-size: 15px;
}
.footer {
  position: absolute;
  bottom: 0px;
  left: 0px;
  width: 1271px;
  height: 50px;
  border-top: 1px solid rgb(2, 40, 120);
}
.footer1 {
  float: left;
  width: 244px;
  height: 50px;
  border-right: 1px solid rgb(2, 40, 120);
  background-color: rgb(76, 116, 181);
  line-height: 50px;
  color: rgb(255, 255, 255);
  font-size: 12px;
}
.footer2 {
  // position: absolute;
  // bottom: 0px;
  // left: 100px;
  float: left;
  width: 224px;
  height: 50px;
  border-right: 1px solid rgb(2, 40, 120);
  background-color: rgb(135, 163, 207);
  line-height: 50px;
  color: rgb(2, 40, 120);
  font-size: 12px;
}
.footer3 {
  // position: absolute;
  // bottom: 0px;
  // left: 200px;
  float: left;
  width: 284px;
  height: 50px;
  border-right: 1px solid rgb(2, 40, 120);
  background-color: rgb(255, 255, 255);
  line-height: 50px;
  color: rgb(2, 40, 120);
  font-size: 12px;
}
.footer4 {
  // position: absolute;
  // bottom: 0px;
  // left: 300px;
  float: left;
  width: 224px;
  height: 50px;
  border-right: 1px solid rgb(2, 40, 120);
  background-color: rgb(135, 163, 207);
  line-height: 50px;
  color: rgb(2, 40, 120);
  font-size: 12px;
}
.footer5 {
  // position: absolute;
  // bottom: 0px;
  // left: 400px;
  float: left;
  width: 255px;
  height: 50px;
  background-color: rgb(255, 255, 255);
  line-height: 50px;
  color: rgb(2, 40, 120);
  font-size: 12px;
}
.brand1 {
  position: absolute;
  top: 40px;
  left: 138px;
  font-size: 18px;
}
.brand2 {
  position: absolute;
  top: 40px;
  left: 352px;
  font-size: 18px;
}
.brand3 {
  position: absolute;
  top: 40px;
  left: 570px;
  font-size: 18px;
}
.brand4 {
  position: absolute;
  top: 40px;
  left: 770px;
  font-size: 18px;
}
.brand5 {
  position: absolute;
  top: 40px;
  left: 970px;
  font-size: 18px;
}

.list1 {
  position: absolute;
  top: 80px;
  left: 136px;
  height: 310px;
  width: 200px;
  border-left: 1px solid rgb(2, 40, 120);
}
.list11 {
  position: absolute;
  top: 80px;
  left: 295px;
  height: 250px;
  width: 20px;
}
.list11Span {
  display: block;
  height: 20px;
  margin-top: 10px;
}

.list2 {
  position: absolute;
  top: 80px;
  left: 350px;
  height: 310px;
  width: 200px;
  border-left: 1px solid rgb(2, 40, 120);
}
.list22 {
  position: absolute;
  top: 80px;
  left: 506px;
  height: 250px;
  width: 20px;
}
.progress2 {
  padding-left: 0px;
}
/deep/.progress2 > .progress-bar__inner {
  background-color: red;
}
.list3 {
  position: absolute;
  top: 80px;
  left: 570px;
  height: 310px;
  width: 200px;
  border-left: 1px solid rgb(2, 40, 120);
}
.list33 {
  position: absolute;
  top: 80px;
  right: 520px;
  height: 250px;
  width: 20px;
}
.list4 {
  position: absolute;
  top: 80px;
  left: 770px;
  height: 310px;
  width: 200px;
  border-left: 1px solid rgb(2, 40, 120);
}
.list44 {
  position: absolute;
  top: 80px;
  right: 322px;
  height: 250px;
  width: 20px;
}
.list5 {
  position: absolute;
  top: 80px;
  left: 970px;
  height: 310px;
  width: 200px;
  border-left: 1px solid rgb(2, 40, 120);
}
.list55 {
  position: absolute;
  top: 80px;
  right: 115px;
  height: 250px;
  width: 20px;
}
.progress3 {
  padding-left: 0px;
}
.chart-container {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 345px;
  height: 345px;
  top: 0px;
  left: -5px;
  background-color: rgba(0, 0, 0, 0);
}
.chart-container1 {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 345px;
  height: 345px;
  top: 0px;
  left: 291px;
  background-color: rgba(0, 0, 0, 0);
}
.chart-container2 {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 345px;
  height: 345px;
  top: 0px;
  left: 587px;
  background-color: rgba(0, 0, 0, 0);
}
.headers {
  position: absolute;
  width: 369px;
  height: 30px;
  border: 1px solid rgb(81, 82, 84);
  border-bottom: none;
  border-left: none;
  top: 200px;
  right: 238px;
}
.header1 {
  position: absolute;
  width: 185px;
  height: 15px;
  border-right: 1px solid rgb(81, 82, 84);
  border-bottom: 1px solid rgb(81, 82, 84);
  top: 0px;
  left: 0px;
}
.header2 {
  position: absolute;
  width: 185px;
  height: 15px;
  border-right: 1px solid rgb(81, 82, 84);
  bottom: 0px;
  left: 0px;
}
.header3 {
  position: absolute;
  width: 184px;
  height: 15px;
  border-bottom: 1px solid rgb(81, 82, 84);
  top: 0px;
  right: 0px;
}
.header4 {
  position: absolute;
  width: 184px;
  height: 15px;
  bottom: 0px;
  right: 0px;
}
.headerSpan {
  font-size: 12px;
  font-weight: 900px;
  vertical-align: 15px;
}
.img1 {
  position: absolute;
  height: 14%;
  top: 180px;
  left: 140px;
}
.img2 {
  position: absolute;
  height: 14%;
  top: 178px;
  left: 435px;
}
.img3 {
  position: absolute;
  height: 14%;
  top: 177px;
  right: 112px;
}

/deep/.el-input__inner {
  width: 100px;
}
.el-select {
  position: absolute;
  top: 20px;
  right: 50px;
}
/deep/[data-v-16290e53] .el-progress-bar__outer {
  // height: 1.4vw !important;
}
.BarChart1 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 0px;
  background-color: rgba(0, 0, 0, 0);
}
.BarChart2 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 152px;
  background-color: rgba(0, 0, 0, 0);
}
.BarChart3 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 382px;
  background-color: rgba(0, 0, 0, 0);
}
.BarChart4 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 612px;
  background-color: rgba(0, 0, 0, 0);
}
.BarChart5 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 842px;
  background-color: rgba(0, 0, 0, 0);
}
</style>