<template>
  <div class="wrapper">
    <br /><br />
    <el-row>
      <el-col :offset="10">
        <el-button icon="el-icon-download" @click="downloadButton"
          >download</el-button
        >
      </el-col>
    </el-row>
    <div class="select">
      <el-button class="select1" @click="btn1">
        <span>Vehicle ratings</span>
      </el-button>
      <el-button class="select2" @click="btn2">
        <span>Forum discussions</span>
      </el-button>
      <el-button class="select3" @click="btn3">
        <span>TextNN</span>
      </el-button>
    </div>
    <div class="headers" v-show="headers">
      <div class="header1"><span class="headerSpan">Timeframe</span></div>
      <div class="header2">
        <span class="headerSpan">Total posts analysed</span>
      </div>
      <div class="header3"><span class="headerSpan">Q2/2021</span></div>
      <div class="header4"><span class="headerSpan">25,200</span></div>
    </div>
    <div class="koubieHeaders" v-show="koubeiHeaders">
      <div class="header2">
        <span class="headerSpan">Total posts analysed</span>
      </div>
      <div class="header4">
        <span class="headerSpan">{{ koubeiNum }}</span>
      </div>
    </div>
    <div class="show1" v-show="show1">
      <span class="title">VEHICLE RATING</span>
      <span class="brand1">{{ brand1Datas.name }}</span>
      <span class="brand2">{{ brand2Datas.name }}</span>
      <span class="brand3">{{ brand3Datas.name }}</span>
      <span class="brand4">{{ brand4Datas.name }}</span>
      <span class="brand5">{{ brand5Datas.name }}</span>

      <span class="comment_percent_brand1">CUSTOMER SENTIMENTS</span>
      <span class="comment_percent_brand2">CUSTOMER SENTIMENTS</span>

      <span class="comment_percent_PNN_brand1">Positive Negative Neutral</span>
      <span class="comment_percent_PNN_brand2">Positive Negative Neutral</span>


      <div id="barChart1" class="BarChart1" v-show="barChar1Show"></div>

      <div id="comment_percent_barChart1" class="comment_percent_BarChart1" v-show="barChar1Show"></div>

      <div id="barChart2" class="BarChart2" v-show="barChar2Show"></div>

      <div id="comment_percent_barChart2" class="comment_percent_BarChart2" v-show="barChar1Show"></div>

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
    <div class="show2" v-show="show2">
      <span class="title">FORUM DISCUSSIONS</span>
      <!-- <span class="brand21">{{brand1Datas.carseries}}</span>
         <span class="brand22">{{brand2Datas.carseries}}</span>
         <span class="brand23">{{brand3Datas.carseries}}</span> -->
      <div id="pieChart" class="chart-container"></div>
      <div id="pieChart1" class="chart-container1"></div>
      <div id="pieChart2" class="chart-container2"></div>

      <div id="pieChart3" v-show="pie3show" class="chart-container3"></div>
      <div id="pieChart4" v-show="pie4show" class="chart-container4"></div>
      <div id="pieChart5" v-show="pie5show" class="chart-container5"></div>
      <img class="img1" :src="img1" />
      <img class="img2" :src="img2" />
      <img class="img3" :src="img3" />
    </div>
    <div class="show3" v-show="show3">
      <br><br>
      <span class="title">Text NN</span>
      <el-col :offset="10">
        <el-button @click="TextNNButton">TextNN Test</el-button>
      </el-col>
      <br><br><br>
      <el-row>
        <el-col :offset="1">
          <el-table
            :data="tableData"
            style="width: 90%"
            :row-class-name="tableRowClassName"
          >
            <el-table-column prop="brand" label="品牌" width="150"> </el-table-column>
            <el-table-column prop="name" label="车型" width="120"> </el-table-column>
            <el-table-column prop="comment" label="评论" :show-overflow-tooltip = "true"> </el-table-column>
            <el-table-column prop="emotion" label="情感正负中" width="100"> </el-table-column>
            <el-table-column prop="positiveNums" label="正个数" width="100"> </el-table-column>
            <el-table-column prop="negativeNums" label="负个数" width="100"> </el-table-column>
            <el-table-column prop="middleNums" label="中个数" width="100"> </el-table-column>
          </el-table>
        </el-col>

      </el-row>
    </div>
  </div>
</template>
<script>
import Echarts from "echarts";
import fileDownload from "js-file-download";

export default {
  data() {
    return {
      options: [{}],
      value: "",
      isselect: "",
      pie3show: false,
      pie4show: false,
      pie5show: false,

      show1: true,
      show2: false,
      show3: false,
      koubeiHeaders: true,
      headers: false,
      brand1Num: 0,
      brand2Num: 0,
      brand3Num: 0,
      brand4Num: 0,
      brand5Num: 0,
      koubeiNum: 0,
      select1: "",
      select2: [],
      select3: [],
      select1Brand: "",
      select2Brand: "",
      select3Brand: "",
      select4Brand: "",
      select5Brand: "",
      list1style: "",
      list2style: "",
      list3style: "",
      list4style: "",
      list5style: "",

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
      img1: "",
      img2: "",
      img3: "",
      pieCharts: null,
      pieCharts1: null,
      pieCharts2: null,
      ieCharts3: null,
      pieCharts4: null,
      pieCharts5: null,
      pieOption: {
        title: {
          text: "",
          show: false,
          left: "center",
          top: "15%",
          textStyle: {
            fontSize: 13,
          },
        },
        color: [
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
        ],
        tooltip: {
          trigger: "item",
          // formatter: "{a} <br/>{b}: {c} ({d}%)"
          formatter: "{b}:{c}%",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["20%", "40%"],
            center: ["50%", "60%"],
            label: {
              normal: {
                show: true,
                //   formatter: '{b}: {c}({d}%)', //自定义显示格式(b:name, c:value, d:百分比)
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [
              // {},{},{},{},{},{},{},{},{},{},
              // {},{},{},{},{},{},{},{},{},{},
              // {},{},{},{},{},{},{},{},{},{},
              { value: 29.5, name: "Appealing exterior" },
              { value: 12.2, name: "Appealing interior" },
              { value: 5.4, name: "Power" },
              { value: 5.1, name: "Comfort" },
              { value: 3.7, name: "Low fuel consumption" },
              { value: 3.1, name: "Large space" },
              { value: 1.7, name: "Good maneuverability" },
              { value: 1.4, name: "Good insulation" },
              { value: 1.4, name: "Many options" },
              { value: 1.0, name: "Safety" },

              { value: 10.8, name: "Strange sounds" },
              { value: 6.8, name: "Transmission problems" },
              { value: 4.4, name: "Uncomfortable" },
              { value: 3.7, name: "Bad insulation" },
              { value: 3.4, name: "Engine problems" },

              { value: 2.0, name: "Strange smell" },
              { value: 1.7, name: "Unappealing exterior" },
              { value: 1.0, name: "High fuel consumption" },
              { value: 0.7, name: "Small space" },
              { value: 0.7, name: "Brakes malfunction" },
              { value: 0.3, name: "Interior problems" },
            ],
          },
        ],
      },
      pieOption1: {
        title: {
          text: "",
          show: false,
          left: "center",
          top: "15%",
          textStyle: {
            fontSize: 13,
          },
        },
        color: [
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
        ],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["20%", "40%"],
            center: ["50%", "60%"],
            label: {
              normal: {
                show: true,
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              //  { value: 7.9, name: 'Appealing exterior' },
              //  { value: 2.3, name: 'Appealing interior' },
              //  { value: 1.6, name: 'Large space' },
              //  { value: 1.2, name: 'Good insulation' },
              //  { value: 1.1, name: 'Low fuel consumption' },

              //  { value: 0.9, name: 'Comfort' },
              //  { value: 0.5, name: 'Good maneuverability' },
              //  { value: 0.2, name: 'Many options' },
              //  { value: 0.2, name: 'Power' },
              //  { value: 0.2, name: 'Safety' },

              //  { value: 39.3, name: 'Strange sounds' },
              //  { value: 9.9, name: 'Uncomfortable' },
              //  { value: 8.1, name: 'Engine problems' },
              //  { value: 7.9, name: 'Transmission problems' },
              //  { value: 3.9, name: 'Strange smell' },

              //  { value: 3.0, name: 'Bad insulation' },
              //  { value: 2.8, name: 'High fuel consumption' },
              //  { value: 2.3, name: 'Unappealing interior' },
              //  { value: 1.9, name: '4S not optimal' },
              //  { value: 1.6, name: 'Interior problems' },

              //  { value: 1.2, name: 'Brakes malfunction' },
              //  { value: 1.1, name: 'Oil leakage' },
              //  { value: 0.9, name: 'Unappealing exterior' },
            ],
          },
        ],
      },
      pieOption2: {
        title: {
          text: "",
          show: false,
          left: "center",
          top: "15%",
          textStyle: {
            fontSize: 13,
          },
        },
        color: [
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(165,184,225)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
          "rgb(53,91,183)",
        ],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["20%", "40%"],
            center: ["50%", "60%"],
            label: {
              normal: {
                show: true,
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              //   { value: 30.4, name: 'Appealing exterior' },
              //   { value: 10.7, name: 'Appealing interior' },
              //   { value: 7.1, name: 'Large space' },
              //   { value: 6.3, name: 'Power' },
              //   { value: 6.3, name: 'Low fuel consumption' },
              //   { value: 2.0, name: 'Good insulation' },
              //   { value: 1.2, name: 'Comfort' },

              //   { value: 0.4, name: 'Many options' },
              //   { value: 8.3, name: 'Uncomfortable' },
              //   { value: 5.5, name: 'Strange smell' },
              //   { value: 5.1, name: 'Unappealing exterior' },
              //   { value: 4.7, name: 'Strange sounds' },
              //   { value: 3.2, name: 'Unappealing interior' },
              //   { value: 2.4, name: 'Water leakage' },

              //   { value: 1.6, name: 'Bad insulation' },
              //   { value: 1.6, name: 'Limited configuration' },
              //   { value: 1.2, name: '4S not optimal' },
              //   { value: 0.8, name: 'Interior problems' },
              //   { value: 0.8, name: 'Small space' },
              //   { value: 0.4, name: 'High fuel consumption' },
            ],
          },
        ],
      },
      pieOption3: {
        title: {
          text: "",
          left: "center",
          top: "1%",
          textStyle: {
            fontSize: 13,
          },
        },
        // color:['rgb(53,91,183)','rgb(53,91,183)','rgb(53,91,183)','rgb(53,91,183)','rgb(53,91,183)','rgb(53,91,183)',],
        color: [],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["", "60%"],
            center: ["50%", "46%"],
            label: {
              normal: {
                show: true,
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              {},
              //   { value: 4.4, name: 'Attractive rear lights' },
              //   { value: 4.4, name: 'Attractive rear' },
              //   { value: 4.4, name: 'Attractive front lights' },
              //   { value: 2.2, name: 'Fashionable front' },
            ],
          },
        ],
      },
      pieOption4: {
        title: {
          text: "",
          left: "center",
          top: "1%",
          textStyle: {
            fontSize: 13,
          },
        },
        color: [],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["", "60%"],
            center: ["50%", "46%"],
            label: {
              normal: {
                show: true,
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [{}, {}, {}, {}, {}, {}, {}, {}, {}, {}],
          },
        ],
      },
      pieOption5: {
        title: {
          text: "",
          left: "center",
          top: "15%",
          textStyle: {
            fontSize: 13,
          },
        },
        color: [],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },
        series: [
          {
            name: "",
            type: "pie",
            radius: ["", "60%"],
            center: ["50%", "46%"],
            label: {
              normal: {
                show: true,
                formatter: function (v) {
                  let text =
                    v.name.split(" ").join("\n") +
                    "(" +
                    Math.round(v.percent) +
                    "%)";
                  return text;
                },
                textStyle: {
                  fontWeight: 900,
                  fontSize: 7,
                },
              },
            },
            itemStyle: {
              borderWidth: 1,
              borderColor: "#fff",
            },
            data: [{}, {}, {}, {}, {}, {}, {}, {}, {}, {}],
          },
        ],
      },
      tableData: [],

      // 柱状图的数据
      barCharts1: null,
      barCharts2: null,
      barCharts3: null,
      barCharts4: null,
      barCharts5: null,
      // 百分比柱状图
      comment_percent_barChart1: null,
      comment_percent_barChart2: null,

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
      comment_percent_barOption1: {
        // tooltip: {
        //   trigger: "axis",
        //   axisPointer: {
        //     type: "shadow",
        //   },
        // },
        textStyle: {
          fontSize: 10,
          color: '#000000'
        },
        grid: {
          // left: '3%',
          // right: '4%',
          // bottom: '3%',
          // containLabel: true
          width: "10%",
          left: "6%",
        },
        xAxis: {
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
            fontSize: 12,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          // 第一列
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              // { value: 54, itemStyle: { color: "#c5cfd7" } },
              // { value: 82, itemStyle: { color: "#c5cfd7" } },
              // { value: 90, itemStyle: { color: "#c5cfd7" } },
              // { value: 92, itemStyle: { color: "#c5cfd7" } },
              // { value: 89, itemStyle: { color: "#c5cfd7" } },
              // { value: 78, itemStyle: { color: "#c5cfd7" } },
              // { value: 72, itemStyle: { color: "#c5cfd7" } },
              // { value: 82, itemStyle: { color: "#c5cfd7" } },
              // { value: 55, itemStyle: { color: "#c5cfd7" } },
              // { value: 54, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  // position: 'top',
                  formatter: '{c}%'
                }
              }
            },
          },
          // 第一列间隙
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
            ],
            label: {
              show: false,
            }
          },
          // 第二列
          {
            name: "Negative",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [2, 2, 2, 2, 2, 2, 2, 2, 2, 2],
            data: [
              // { value: 44, itemStyle: { color: "#c5cfd7" } },
              // { value: 15, itemStyle: { color: "#c5cfd7" } },
              // { value: 9, itemStyle: { color: "#c5cfd7" } },
              // { value: 7, itemStyle: { color: "#c5cfd7" } },
              // { value: 10, itemStyle: { color: "#c5cfd7" } },
              // { value: 12, itemStyle: { color: "#c5cfd7" } },
              // { value: 8, itemStyle: { color: "#c5cfd7" } },
              // { value: 5, itemStyle: { color: "#c5cfd7" } },
              // { value: 26, itemStyle: { color: "#c5cfd7" } },
              // { value: 44, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  // position: 'center',
                  formatter: '{c}%'
                }
              }
            },
          },
          // 第二列间隙
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
            ],
            label: {
              show: false,
            }
          },
          // 第三列
          {
            name: "Neutral",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            data: [
              // { value: 2, itemStyle: { color: "#c5cfd7" } },
              // { value: 3, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 10, itemStyle: { color: "#c5cfd7" } },
              // { value: 20, itemStyle: { color: "#c5cfd7" } },
              // { value: 13, itemStyle: { color: "#c5cfd7" } },
              // { value: 19, itemStyle: { color: "#c5cfd7" } },
              // { value: 2, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  position: 'right',
                  formatter: '{c}%'
                }
              }
            },
          },
        ],
      },
      comment_percent_barOption2: {
        // tooltip: {
        //   trigger: "axis",
        //   axisPointer: {
        //     type: "shadow",
        //   },
        // },
        textStyle: {
          fontSize: 10,
          color: '#000000'
        },
        grid: {
          // left: '3%',
          // right: '4%',
          // bottom: '3%',
          // containLabel: true
          width: "10%",
          left: "6%",
        },
        xAxis: {
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
            fontSize: 12,
          },
          axisTick: {
            show: false, //不显示坐标轴刻度线
          },
        },
        series: [
          // 第一列
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              // { value: 0, itemStyle: { color: "#c5cfd7" } },
              // { value: 82, itemStyle: { color: "#c5cfd7" } },
              // { value: 90, itemStyle: { color: "#c5cfd7" } },
              // { value: 92, itemStyle: { color: "#c5cfd7" } },
              // { value: 89, itemStyle: { color: "#c5cfd7" } },
              // { value: 78, itemStyle: { color: "#c5cfd7" } },
              // { value: 72, itemStyle: { color: "#c5cfd7" } },
              // { value: 82, itemStyle: { color: "#c5cfd7" } },
              // { value: 55, itemStyle: { color: "#c5cfd7" } },
              // { value: 54, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  // position: 'top',
                  formatter: '  {c}%  '
                }
              }
            },
          },
          // 第一列间隙
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
            ],
            label: {
              show: false,
            }
          },
          // 第二列
          {
            name: "Negative",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [2, 2, 2, 2, 2, 2, 2, 2, 2, 2],
            data: [
              // { value: 0, itemStyle: { color: "#c5cfd7" } },
              // { value: 15, itemStyle: { color: "#c5cfd7" } },
              // { value: 9, itemStyle: { color: "#c5cfd7" } },
              // { value: 7, itemStyle: { color: "#c5cfd7" } },
              // { value: 10, itemStyle: { color: "#c5cfd7" } },
              // { value: 12, itemStyle: { color: "#c5cfd7" } },
              // { value: 8, itemStyle: { color: "#c5cfd7" } },
              // { value: 5, itemStyle: { color: "#c5cfd7" } },
              // { value: 26, itemStyle: { color: "#c5cfd7" } },
              // { value: 44, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  // position: 'center',
                  formatter: '{c}%'
                }
              }
            },
          },
          // 第二列间隙
          {
            name: "Positive",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            // data: [1, 2, 3, 1, 1, 1, 1, 1, 1, 1],
            data: [
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
              { value: 1, itemStyle: { color: "#FFFAFA" } },
            ],
            label: {
              show: false,
            }
          },
          // 第三列
          {
            name: "Neutral",
            type: "bar",
            stack: "total",
            label: {
              show: true,
            },
            emphasis: {
              focus: "series",
            },
            data: [
              // { value: 0, itemStyle: { color: "#c5cfd7" } },
              // { value: 3, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 1, itemStyle: { color: "#c5cfd7" } },
              // { value: 10, itemStyle: { color: "#c5cfd7" } },
              // { value: 20, itemStyle: { color: "#c5cfd7" } },
              // { value: 13, itemStyle: { color: "#c5cfd7" } },
              // { value: 19, itemStyle: { color: "#c5cfd7" } },
              // { value: 2, itemStyle: { color: "#c5cfd7" } },
            ],
            itemStyle: {
              normal: {
                label: {
                  show: true,
                  position: 'right',
                  formatter: '{c}%'
                }
              }
            },
          },
        ],
      },
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.pieCharts = Echarts.init(document.getElementById("pieChart"));
      this.pieCharts.setOption(this.pieOption);
      this.pieCharts.on("mouseout", (data) => {
        this.pie3show = false;
      });
      this.pieCharts.on("mouseover", (data) => {
        if (data.nme != this.isselect) {
          //请求数据
          this.axios({
            url: "/api/piedatas/queryAll",
            method: "POST",
            params: {
              brand: this.pieOption.title.text,
              category: data.name,
            },
          }).then((resp) => {
            if (resp.data[0].commenttype == "正面评论") {
              this.pieOption3.color[0] = "rgb(53,91,183)";
            } else {
              this.pieOption3.color[0] = "rgb(165,184,225)";
            }
            //清空data
            for (let i = 0; i <= 10; i++) {
              this.pieOption3.series[0].data[i] = {};
            }
            for (let i = 0; i < resp.data.length; i++) {
              this.pieOption3.series[0].data[i].value =
                resp.data[i].detailsrate;
              this.pieOption3.series[0].data[i].name = resp.data[i].details;
            }
            this.pieCharts3.setOption(this.pieOption3);
          });
        }
        this.pie3show = true;
        this.isselect = data.name;
      });

      this.pieCharts1 = Echarts.init(document.getElementById("pieChart1"));
      this.pieCharts1.setOption(this.pieOption1);
      this.pieCharts1.on("mouseout", (data) => {
        this.pie4show = false;
      });
      this.pieCharts1.on("mouseover", (data) => {
        if (data.name != this.isselect) {
          //请求数据
          this.axios({
            url: "/api/piedatas/queryAll",
            method: "POST",
            params: {
              brand: this.pieOption1.title.text,
              category: data.name,
            },
          }).then((resp) => {
            if (resp.data[0].commenttype == "正面评论") {
              this.pieOption4.color[0] = "rgb(53,91,183)";
            } else {
              this.pieOption4.color[0] = "rgb(165,184,225)";
            }
            //清空data
            for (let i = 0; i <= 10; i++) {
              this.pieOption4.series[0].data[i] = {};
            }
            for (let i = 0; i < resp.data.length; i++) {
              this.pieOption4.series[0].data[i].value =
                resp.data[i].detailsrate;
              this.pieOption4.series[0].data[i].name = resp.data[i].details;
            }
            this.pieCharts4.setOption(this.pieOption4);
          });
        }
        this.pie4show = true;
        this.isselect = data.name;
      });

      this.pieCharts2 = Echarts.init(document.getElementById("pieChart2"));
      this.pieCharts2.setOption(this.pieOption2);
      this.pieCharts2.on("mouseout", (data) => {
        this.pie5show = false;
      });
      this.pieCharts2.on("mouseover", (data) => {
        if (data.name != this.isselect) {
          //请求数据
          this.axios({
            url: "/api/piedatas/queryAll",
            method: "POST",
            params: {
              brand: this.pieOption2.title.text,
              category: data.name,
            },
          }).then((resp) => {
            if (resp.data[0].commenttype == "正面评论") {
              this.pieOption5.color[0] = "rgb(53,91,183)";
            } else {
              this.pieOption5.color[0] = "rgb(165,184,225)";
            }
            //清空data
            for (let i = 0; i <= 10; i++) {
              this.pieOption5.series[0].data[i] = {};
            }
            for (let i = 0; i < resp.data.length; i++) {
              this.pieOption5.series[0].data[i].value =
                resp.data[i].detailsrate;
              this.pieOption5.series[0].data[i].name = resp.data[i].details;
            }
            this.pieCharts5.setOption(this.pieOption5);
          });
        }
        this.pie5show = true;
        this.isselect = data.name;
      });

      this.pieCharts3 = Echarts.init(document.getElementById("pieChart3"));
      this.pieCharts3.setOption(this.pieOption3);

      this.pieCharts4 = Echarts.init(document.getElementById("pieChart4"));
      this.pieCharts4.setOption(this.pieOption4);

      this.pieCharts5 = Echarts.init(document.getElementById("pieChart5"));
      this.pieCharts5.setOption(this.pieOption5);


      // 这里初始化，然后再getbrand函数中设置this.barCharts1.setOption(this.barOption1);
      this.barCharts1 = Echarts.init(document.getElementById("barChart1"));
      this.barCharts1.setOption(this.barOption1);

      this.barCharts2 = Echarts.init(document.getElementById("barChart2"));
      this.barCharts2.setOption(this.barOption2);

      this.barCharts3 = Echarts.init(document.getElementById("barChart3"));
      this.barCharts3.setOption(this.barOption3);

      this.barCharts4 = Echarts.init(document.getElementById("barChart4"));
      this.barCharts4.setOption(this.barOption4);

      this.barCharts5 = Echarts.init(document.getElementById("barChart5"));
      this.barCharts5.setOption(this.barOption5);

      // 百分比柱状图数据
      this.comment_percent_barChart1 = Echarts.init(document.getElementById("comment_percent_barChart1"));
      this.comment_percent_barChart1.setOption(this.comment_percent_barOption1)

      // 百分比柱状图数据
      this.comment_percent_barChart2 = Echarts.init(document.getElementById("comment_percent_barChart2"));
      this.comment_percent_barChart2.setOption(this.comment_percent_barOption2)

      window.addEventListener("resize", this.handleResize);

    });
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

    this.getComment_percent_barOption1();
    this.getComment_percent_barOption2();

    this.getAllEmotionQuery()

    this.getdata();
    
  },
  watch: {
    value(newvalue, oldvalue) {
      this.$router.push({
        path: "/productEvaluationByCarModel",
        query: {
          select1: this.select2,
          select2: this.select2,
          select3: this.select3,
        },
      });
    },
    brand1Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue
    },
    brand2Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue
    },
    brand3Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue
    },
    brand4Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue
    },
    brand5Num(newvalue, oldvalue) {
      this.koubeiNum = this.koubeiNum + newvalue - oldvalue
    },
  },
  methods: {
    tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      },
    getpiedata(carbrand, pieOption, pieChartsNum) {
      this.axios({
        url: "/api/piedatas/queryAllcategoryByBrand",
        method: "POST",
        params: { brand: carbrand },
      }).then((resp) => {
        pieOption.title.text = resp.data.result[0].brand;
        for (let i = 0; i < resp.data.result.length; i++) {
          //数据赋值
          pieOption.series[0].data[i].value = resp.data.result[i].categoryrate;
          pieOption.series[0].data[i].name = resp.data.result[i].category;
          //change color
          if (resp.data.result[i].commenttype == "正面评论") {
            pieOption.color[i] = "rgb(53,91,183)";
          } else {
            pieOption.color[i] = "rgb(165,184,225)";
          }
        }
        //更新饼图 、 设置车的图标
        if (pieChartsNum == 0) {
          this.pieCharts.setOption(pieOption);
          this.changeCarImg(resp.data.result[0].brand, 0);
        }
        if (pieChartsNum == 1) {
          this.pieCharts1.setOption(pieOption);
          this.changeCarImg(resp.data.result[0].brand, 1);
        }
        if (pieChartsNum == 2) {
          this.pieCharts2.setOption(pieOption);
          this.changeCarImg(resp.data.result[0].brand, 2);
        }
      });
    },
    changeCarImg(brand, imgType) {
      if (imgType == 0) {
        if (brand.indexOf("MERCEDES_BENZ") == 0) {
          this.img1 = require("../assets/images/benchi.png");
        } else if (brand.indexOf("BMW") == 0) {
          this.img1 = require("../assets/images/baoma.png");
        } else if (brand.indexOf("AUDI") == 0) {
          this.img1 = require("../assets/images/aodi.png");
        } else if (brand.indexOf("SAIC_VOLKSWAGEN") == 0) {
          this.img1 = require("../assets/images/shangqi.png");
        } else if (brand.indexOf("CADILLAC") == 0) {
          this.img1 = require("../assets/images/kaidilake.png");
        } else if (brand.indexOf("LAND_ROVER") == 0) {
          this.img1 = require("../assets/images/luhu.png");
        }
      } else if (imgType == 1) {
        if (brand.indexOf("MERCEDES_BENZ") == 0) {
          this.img2 = require("../assets/images/benchi.png");
        } else if (brand.indexOf("BMW") == 0) {
          this.img2 = require("../assets/images/baoma.png");
        } else if (brand.indexOf("AUDI") == 0) {
          this.img2 = require("../assets/images/aodi.png");
        } else if (brand.indexOf("SAIC_VOLKSWAGEN") == 0) {
          this.img2 = require("../assets/images/shangqi.png");
        } else if (brand.indexOf("CADILLAC") == 0) {
          this.img2 = require("../assets/images/kaidilake.png");
        } else if (brand.indexOf("LAND_ROVER") == 0) {
          this.img2 = require("../assets/images/luhu.png");
        }
      } else if (imgType == 2) {
        if (brand.indexOf("MERCEDES_BENZ") == 0) {
          this.img3 = require("../assets/images/benchi.png");
        } else if (brand.indexOf("BMW") == 0) {
          this.img3 = require("../assets/images/baoma.png");
        } else if (brand.indexOf("AUDI") == 0) {
          this.img3 = require("../assets/images/aodi.png");
        } else if (brand.indexOf("SAIC_VOLKSWAGEN") == 0) {
          this.img3 = require("../assets/images/shangqi.png");
        } else if (brand.indexOf("CADILLAC") == 0) {
          this.img3 = require("../assets/images/kaidilake.png");
        } else if (brand.indexOf("LAND_ROVER") == 0) {
          this.img3 = require("../assets/images/luhu.png");
        }
      }
    },
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
    // 获取brand数据
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
       
        // 获取口碑数据
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select2,
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
          this.select1Brand = resp.data.result.brand;

          this.barCharts1.setOption(this.barOption1);
          this.barChar1Show = true

          this.getpiedata(this.select1Brand, this.pieOption, 0);
        });

        
      } else {
        this.list1style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand2Datas() {
      
        // 获取口碑数据
      if (this.select3.length >= 1) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[0],
            date: this.value,
          },
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
          this.select2Brand = resp.data.result.brand;

          // 更新柱状图
          this.barCharts2.setOption(this.barOption2);
          this.barChar2Show = true

          this.getpiedata(this.select2Brand, this.pieOption1, 1);
        });

        
      } else {
        this.list2style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand3Datas() {
      
        // 获取口碑数据
      if (this.select3.length >= 2) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[1],
            date: this.value,
          },
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
          this.select3Brand = resp.data.result.brand;

          // 更新柱状图
          this.barCharts3.setOption(this.barOption3);
          this.barChar3Show = true

          this.getpiedata(this.select3Brand, this.pieOption2, 2);
        });

        
      }
    },
    getBrand4Datas() {
      
        // 获取口碑数据
      if (this.select3.length >= 3) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[2],
            date: this.value,
          },
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
          this.select4Brand = resp.data.result.brand;

          // 更新柱状图
          this.barCharts4.setOption(this.barOption4);
          this.barChar4Show = true
        });
      }
    },
    getBrand5Datas() {
      
        // 获取口碑数据
      if (this.select3.length >= 4) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[3],
            date: this.value,
          },
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
          this.select5Brand = resp.data.result.brand;

          // 更新柱状图
          this.barCharts5.setOption(this.barOption5);
          this.barChar5Show = true
        });
      }
    },

    getComment_percent_barOption1() {
      if (this.select2 != "") {
        // 获取评论百分比的数据
        this.axios({
          url: "/api/koubei/selectEmotionByBrandAndName",
          method: "GET",
          params: {
            name: this.select2,
            date: this.value,
          },
        }).then((resp) => {
          let data = resp.data.result
          // 第一列的数据
          this.comment_percent_barOption1.series[0].data = [];

          this.comment_percent_barOption1.series[0].data.push({
            value: data.optionsandfeaturesPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.comfortPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.fuelConsumptionPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.maneuverabilityPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.powerPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.valueformoneyPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.carspacePositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.interiorPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.exteriorPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption1.series[0].data.push({
            value: data.overallPositive,
            itemStyle:{color: "#9ec97e" },
          });

          // 第三列的数据
          this.comment_percent_barOption1.series[2].data = [];

          this.comment_percent_barOption1.series[2].data.push({
            value: data.optionsandfeaturesNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.comfortNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.fuelConsumptionNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.maneuverabilityNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.powerNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.valueformoneyNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.carspaceNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.interiorNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.exteriorNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption1.series[2].data.push({
            value: data.overallNegitive,
            itemStyle:{color: "#c5cfd7" },
          });

          // 第五列的数据
          this.comment_percent_barOption1.series[4].data = [];

          this.comment_percent_barOption1.series[4].data.push({
            value: data.optionsandfeaturesNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.comfortNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.fuelConsumptionNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.maneuverabilityNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.powerNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.valueformoneyNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.carspaceNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.interiorNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.exteriorNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption1.series[4].data.push({
            value: data.overallNeutral,
            itemStyle:{color: "#de6e6a" },
          });

          // 当某一行三列的数据都为0，则不显示，并且显示NA
          for (let i = 0; i < 10; i++) {
            let positive =  this.comment_percent_barOption1.series[0].data[i].value;
            let negative =  this.comment_percent_barOption1.series[2].data[i].value;
            let neutral =  this.comment_percent_barOption1.series[4].data[i].value;

            if (positive == 0 && negative == 0 && neutral == 0) {
              this.comment_percent_barOption1.series[0].data[i] = {value: 100,  
              itemStyle: {color: "#FFFAFA"},
              label:{
                show: true,
                formatter: "NA",
              }};
              this.comment_percent_barOption1.series[2].data[i] = {value: 0,  label:{
                show: false,
              }};
              this.comment_percent_barOption1.series[4].data[i] = {value: 0,  label:{
                show: false,
              }}
            }
          }

          this.comment_percent_barChart1.setOption(this.comment_percent_barOption1);
        })
      }
    },
    getComment_percent_barOption2(){
      if (this.select3.length >= 1) {
        this.axios({
          url: "/api/koubei/selectEmotionByBrandAndName",
          method: "GET",
          params: {
            name: this.select3[0],
            date: this.value,
          },
        }).then((resp) => {
          let data = resp.data.result
          this.comment_percent_barOption2.series[0].data = [];

          this.comment_percent_barOption2.series[0].data.push({
            value: data.optionsandfeaturesPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.comfortPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.fuelConsumptionPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.maneuverabilityPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.powerPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.valueformoneyPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.carspacePositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.interiorPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.exteriorPositive,
            itemStyle:{color: "#9ec97e" },
          });
          this.comment_percent_barOption2.series[0].data.push({
            value: data.overallPositive,
            itemStyle:{color: "#9ec97e" },
          });

          // 第三列的数据
          this.comment_percent_barOption2.series[2].data = [];

          this.comment_percent_barOption2.series[2].data.push({
            value: data.optionsandfeaturesNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.comfortNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.fuelConsumptionNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.maneuverabilityNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.powerNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.valueformoneyNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.carspaceNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.interiorNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.exteriorNegitive,
            itemStyle:{color: "#c5cfd7" },
          });
          this.comment_percent_barOption2.series[2].data.push({
            value: data.overallNegitive,
            itemStyle:{color: "#c5cfd7" },
          });

          // 第五列的数据
          this.comment_percent_barOption2.series[4].data = [];

          this.comment_percent_barOption2.series[4].data.push({
            value: data.optionsandfeaturesNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.comfortNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.fuelConsumptionNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.maneuverabilityNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.powerNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.valueformoneyNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.carspaceNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.interiorNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.exteriorNeutral,
            itemStyle:{color: "#de6e6a" },
          });
          this.comment_percent_barOption2.series[4].data.push({
            value: data.overallNeutral,
            itemStyle:{color: "#de6e6a" },
          });

          // 当某一行三列的数据都为0，则不显示，并且显示NA
          for (let i = 0; i < 10; i++) {
            let positive =  this.comment_percent_barOption2.series[0].data[i].value;
            let negative =  this.comment_percent_barOption2.series[2].data[i].value;
            let neutral =  this.comment_percent_barOption2.series[4].data[i].value;

            if (positive == 0 && negative == 0 && neutral == 0) {
              this.comment_percent_barOption2.series[0].data[i] = {value: 100,  
              itemStyle: {color: "#FFFAFA"},
              label:{
                show: true,
                formatter: "NA",
              }};
              this.comment_percent_barOption2.series[2].data[i] = {value: 0,  label:{
                show: false,
              }};
              this.comment_percent_barOption2.series[4].data[i] = {value: 0,  label:{
                show: false,
              }}
            }
          }

          this.comment_percent_barChart2.setOption(this.comment_percent_barOption2);
        })
      }
    },

    reLoadBar() {
      this.barCharts1.setOption(this.barOption1);
      this.barCharts2.setOption(this.barOption2);
      this.barCharts3.setOption(this.barOption3);
      this.barCharts4.setOption(this.barOption4);
      this.barCharts5.setOption(this.barOption5);
    },

    selectChange() {
      // show3的textNN数据变为空
      this.tableData = []

      this.getBrand1Datas();
      this.getBrand2Datas();
      this.getBrand3Datas();
      this.getBrand4Datas();
      this.getBrand5Datas();

      this.getComment_percent_barOption1();
      this.getComment_percent_barOption2();

      this.getAllEmotionQuery()
    },
    getpieOption() {},
    getpieOption1() {},
    getpieOption2() {},



    btn1() {
      this.show1 = true;
      this.show2 = false;
      this.show3 = false;
      this.koubeiHeaders = true;
      this.headers = false;
    },
    btn2() {
      this.show1 = false;
      this.show2 = true;
      this.show3 = false;
      this.koubeiHeaders = false;
      this.headers = true;
    },
    btn3() {
      this.show1 = false;
      this.show2 = false;
      this.show3 = true;
      this.koubeiHeaders = false;
      this.headers = false;
    },
    handleResize() {
      this.pieCharts.resize();

      this.pieCharts1.resize();
      this.pieCharts2.resize();
    },
    downloadButton() {
      // 检查第一个是否为空
      if (this.select2 != null) {
        // 导出第一个excel
        this.axios({
          url: "/api/easyExcel/queryByKoubeiExcelSaveOneMonthDataQuery",
          methods: "POST",
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/json;charset=utf-8",
            accessToken: "niceyoo",
          },
          params: {
            name: this.select2,
            date: this.value,
          },
        }).then((resp) => {
          fileDownload(resp.data, this.select2 + ".xlsx");
        });
      }
      // 检查第二个是否为空
      if (this.select3[0] != null) {
        console.log("select3[0]:" + this.select3[0]);
        // 导出第二个excel
        this.axios({
          url: "/api/easyExcel/queryByKoubeiExcelSaveOneMonthDataQuery",
          methods: "POST",
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/json;charset=utf-8",
            accessToken: "niceyoo",
          },
          params: {
            name: this.select3[0],
            date: this.value,
          },
        }).then((resp) => {
          fileDownload(resp.data, this.select3[0] + ".xlsx");
        });
      }
      // 检查第三个是否为空
      if (this.select3[1] != null) {
        console.log("select3[1]:" + this.select3[1]);
        // 导出第三个excel
        this.axios({
          url: "/api/easyExcel/queryByKoubeiExcelSaveOneMonthDataQuery",
          methods: "POST",
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/json;charset=utf-8",
            accessToken: "niceyoo",
          },
          params: {
            name: this.select3[1],
            date: this.value,
          },
        }).then((resp) => {
          fileDownload(resp.data, this.select3[1] + ".xlsx");
        });
      }
      // 检查第四个是否为空
      if (this.select3[2] != null) {
        console.log("select3[2]:" + this.select3[2]);
        // 导出第四个excel
        this.axios({
          url: "/api/easyExcel/queryByKoubeiExcelSaveOneMonthDataQuery",
          methods: "POST",
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/json;charset=utf-8",
            accessToken: "niceyoo",
          },
          params: {
            name: this.select3[2],
            date: this.value,
          },
        }).then((resp) => {
          fileDownload(resp.data, this.select3[2] + ".xlsx");
        });
      }
      // 检查第五个是否为空
      if (this.select3[3] != null) {
        console.log("select3[3]:" + this.select3[3]);
        // 导出第五个excel
        this.axios({
          url: "/api/easyExcel/queryByKoubeiExcelSaveOneMonthDataQuery",
          methods: "POST",
          responseType: "arraybuffer",
          headers: {
            "Content-Type": "application/json;charset=utf-8",
            accessToken: "niceyoo",
          },
          params: {
            name: this.select3[3],
            date: this.value,
          },
        }).then((resp) => {
          fileDownload(resp.data, this.select3[3] + ".xlsx");
        });
      }
    },
    TextNNButton() {
      this.$router.push({path:'/textNN'})
    },
    emotionQuery(name, date) {
      // 检查第一个是否为空
      // if (this.select2 != null) {
        // 导出第一个excel
        this.axios({
          url: "/api/textNNControl/selectEmotionByBrandAndName",
          method: "GET",
          params: {
            // name: this.select2,
            // date: this.value,
            name: name,
            date: date,
          },
        }).then((resp) => {
          this.tableData.push({
            brand: resp.data.result.brand,
            name: resp.data.result.name,
            comment: resp.data.result.comment.substring(1,2000),
            // comment: '你好饭撒分身乏术了开发商饭撒方式雷\n锋精神疗-法是放假<br>啦</br>放假啦是咖啡就算了弗兰克撒疯了',
            emotion: resp.data.result.emotion,
            positiveNums: resp.data.result.positiveNums,
            negativeNums: resp.data.result.negativeNums,
            middleNums: resp.data.result.middleNums,
          })
        });
      // }
    },
    getAllEmotionQuery() {

      // 获取brand1的emotion
      if (this.select2 != "") {
         // 获取emotion数据
        this.emotionQuery(this.select2, this.value)
      }
    // 获取brand2的emotion
    if (this.select3.length >= 1) {
         // 获取emotion数据
        this.emotionQuery(this.select3[0], this.value)
      }
    // 获取brand3的emotion
    if (this.select3.length >= 2) {
        // 获取emotion数据
        this.emotionQuery(this.select3[1], this.value)
      }
    // 获取brand4的emotion
    if (this.select3.length >= 3) {
         // 获取emotion数据
        this.emotionQuery(this.select3[2], this.value)
      }
    // 获取brand5的emotion
    if (this.select3.length >= 4) {
        // 获取emotion数据
        this.emotionQuery(this.select3[3], this.value)
      }

  },
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
    this.pieCharts.dispose();

    this.pieCharts1.dispose();
    this.pieCharts2.dispose();
  },
};
</script>
<style lang="less" scoped>
.select {
  position: absolute;
  top: 100px;
  left: 100px;
  // width: 530px;
  width: 790px;
  height: 30px;
  border: 1px solid rgb(2, 40, 120);
  border-bottom: none;
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
  // right: 0px;
  left: 250px;
  width: 265px;
  height: 30px;
  border-radius: 0px;
}
.select3 {
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
  top: 130px;
  left: 100px;
  width: 1271px;
  height: 460px;
  border: 1px solid rgb(2, 40, 120);
}
.show3 {
  position: absolute;
  top: 130px;
  left: 100px;
  width: 1271px;
  height: 460px;
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
  // padding-top: 3%;
  // padding-bottom: 3%;
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
  top: 45px;
  left: 138px;
  font-size: 18px;
}
.brand2 {
  position: absolute;
  top: 45px;
  left: 600px;
  font-size: 18px;
}
.brand3 {
  position: absolute;
  top: 45px;
  left: 580px;
  font-size: 18px;
}
.brand4 {
  position: absolute;
  top: 45px;
  left: 810px;
  font-size: 18px;
}
.brand5 {
  position: absolute;
  top: 45px;
  left: 1040px;
  font-size: 18px;
}
.comment_percent_brand1 {
  position: absolute;
  top: 20px;
  left: 338px;
  font-size: 18px;
}
.comment_percent_brand2 {
  position: absolute;
  top: 20px;
  left: 826px;
  font-size: 18px;
}
.comment_percent_PNN_brand1 {
  position: absolute;
  top: 52px;
  left: 370px;
  font-size: 12px;
}
.comment_percent_PNN_brand2 {
  position: absolute;
  top: 52px;
  left: 836px;
  font-size: 12px;
}
.brand21 {
  position: absolute;
  top: 45px;
  left: 120px;
  font-size: 18px;
}
.brand22 {
  position: absolute;
  top: 45px;
  left: 410px;
  font-size: 18px;
}
.brand23 {
  position: absolute;
  top: 45px;
  left: 716px;
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
  top: -5px;
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
  top: -5px;
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
  top: -5px;
  left: 587px;
  background-color: rgba(0, 0, 0, 0);
}
.chart-container3 {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 350px;
  height: 300px;
  top: 280px;
  left: 0px;
  background-color: rgba(0, 0, 0, 0);
}
.chart-container4 {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 350px;
  height: 300px;
  top: 280px;
  left: 300px;
  background-color: rgba(0, 0, 0, 0);
}
.chart-container5 {
  border-radius: 4px;
  background: #fff;
  //   box-shadow: 0 1px 10px 2px rgba(182, 191, 196, 0.5);

  position: absolute;
  width: 350px;
  height: 300px;
  top: 280px;
  left: 600px;
  background-color: rgba(0, 0, 0, 0);
}
.headers {
  position: absolute;
  width: 369px;
  height: 30px;
  border: 1px solid rgb(81, 82, 84);
  border-bottom: none;
  border-left: none;
  top: 100px;
  // left: 632px;
  right: 179px;
}
.koubieHeaders {
  position: absolute;
  width: 369px;
  height: 15px;
  border: 1px solid rgb(81, 82, 84);
  border-bottom: none;
  border-left: none;
  top: 114px;
  // left: 632px;
  right: 179px;
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
  top: 170px;
  left: 137px;
}
.img2 {
  position: absolute;
  height: 14%;
  top: 170px;
  left: 432px;
}
.img3 {
  position: absolute;
  height: 14%;
  top: 170px;
  left: 728px;
}
/deep/.el-input__inner {
  width: 100px;
}
.el-select {
  position: absolute;
  top: 20px;
  right: 50px;
}
/deep/.el-table .warning-row {
    background: oldlace;
  }

/deep/.el-table .success-row {
    background: #f0f9eb;
}

/deep/.el-progress-bar__outer {
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
  left: 396px;
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
.comment_percent_BarChart1 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 246px;
  background-color: rgba(0, 0, 0, 0);
}
.comment_percent_BarChart2 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 10px;
  left: 720px;
  background-color: rgba(0, 0, 0, 0);
}
</style>