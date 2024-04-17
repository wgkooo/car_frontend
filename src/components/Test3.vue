<template>
  <div class="wrapper">
    <br />
    <el-row :gutter="20">
      <el-col>
        <div class="show1">
          <div id="barChart1" class="BarChart1"></div>
          <div id="barChart2" class="BarChart2"></div>
          <div id="barChart3" class="BarChart3"></div>
          <div id="barChart4" class="BarChart4"></div>
          <div id="barChart5" class="BarChart5"></div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import Echarts from "echarts";
export default {
  data() {
    return {
      barCharts1: null,
      barCharts2: null,
      barCharts3: null,
      barCharts4: null,
      barCharts5: null,
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
            show: true, // 是否显示纵坐标的text
            margin: 8,
            fontSize: 12,
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
              { value: 1, itemStyle: { color: "#849fca" } },
              { value: 0.96, itemStyle: { color: "#849fca" } },
              { value: 0.79, itemStyle: { color: "#849fca" } },
              { value: 0.83, itemStyle: { color: "#849fca" } },
              { value: 0.88, itemStyle: { color: "#849fca" } },
              { value: 0.97, itemStyle: { color: "#849fca" } },
              { value: 0.86, itemStyle: { color: "#849fca" } },
              { value: 0.84, itemStyle: { color: "#849fca" } },
              { value: 0.98, itemStyle: { color: "#849fca" } },
              { value: 0.99, itemStyle: { color: "#849fca" } },
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
          boundaryGap: true,
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
          boundaryGap: true,
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
              // { value: 54, itemStyle: { color: "#9ec97e" } },
              { value: 54, itemStyle: { color: "#9ec97e" }, label:{
                show: true,
                formatter: "data",
              } },
              { value: 82, itemStyle: { color: "#9ec97e" } },
              { value: 90, itemStyle: { color: "#9ec97e" } },
              { value: 92, itemStyle: { color: "#9ec97e" } },
              { value: 89, itemStyle: { color: "#9ec97e" } },
              { value: 78, itemStyle: { color: "#9ec97e" } },
              { value: 72, itemStyle: { color: "#9ec97e" } },
              { value: 82, itemStyle: { color: "#9ec97e" } },
              { value: 55, itemStyle: { color: "#9ec97e" } },
              // { value: 54, itemStyle: { color: "#9ec97e" } },
              // {value: 0, label: {
              //   show: true,
              //   formatter: "NA"
              // }}
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
              { value: 101, itemStyle: { color: "#FFFAFA" }, label:{show: true , formatter:'N.A'} },
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
              { value: 44, itemStyle: { color: "#c5cfd7" } },
              { value: 15, itemStyle: { color: "#c5cfd7" } },
              { value: 9, itemStyle: { color: "#c5cfd7" } },
              { value: 7, itemStyle: { color: "#c5cfd7" } },
              { value: 10, itemStyle: { color: "#c5cfd7" } },
              { value: 12, itemStyle: { color: "#c5cfd7" } },
              { value: 8, itemStyle: { color: "#c5cfd7" } },
              { value: 5, itemStyle: { color: "#c5cfd7" } },
              { value: 26, itemStyle: { color: "#c5cfd7" } },
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
              { value: 2, itemStyle: { color: "#de6e6a" } },
              { value: 3, itemStyle: { color: "#de6e6a" } },
              { value: 1, itemStyle: { color: "#de6e6a" } },
              { value: 1, itemStyle: { color: "#de6e6a" } },
              { value: 1, itemStyle: { color: "#de6e6a" } },
              { value: 10, itemStyle: { color: "#de6e6a" } },
              { value: 20, itemStyle: { color: "#de6e6a" } },
              { value: 13, itemStyle: { color: "#de6e6a" } },
              { value: 19, itemStyle: { color: "#de6e6a" } },
              // { value: 2, itemStyle: { color: "#de6e6a" } },
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
              { value: 1, itemStyle: { color: "#849fca" } },
              { value: 0.96, itemStyle: { color: "#849fca" } },
              { value: 0.79, itemStyle: { color: "#849fca" } },
              { value: 0.83, itemStyle: { color: "#849fca" } },
              { value: 0.88, itemStyle: { color: "#849fca" } },
              { value: 0.97, itemStyle: { color: "#849fca" } },
              { value: 0.86, itemStyle: { color: "orange" } },
              { value: 0.84, itemStyle: { color: "#849fca" } },
              { value: 0.98, itemStyle: { color: "#849fca" } },
              { value: 0.99, itemStyle: { color: "#849fca" } },
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
              { value: 1, itemStyle: { color: "#849fca" } },
              { value: 0.96, itemStyle: { color: "#849fca" } },
              { value: 0.79, itemStyle: { color: "#849fca" } },
              { value: 0.83, itemStyle: { color: "#849fca" } },
              { value: 0.88, itemStyle: { color: "#849fca" } },
              { value: 0.97, itemStyle: { color: "#849fca" } },
              { value: 0.86, itemStyle: { color: "orange" } },
              { value: 0.84, itemStyle: { color: "#849fca" } },
              { value: 0.98, itemStyle: { color: "#849fca" } },
              { value: 0.99, itemStyle: { color: "#849fca" } },
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
              { value: 1, itemStyle: { color: "#849fca" } },
              { value: 0.96, itemStyle: { color: "#849fca" } },
              { value: 0.79, itemStyle: { color: "#849fca" } },
              { value: 0.83, itemStyle: { color: "#849fca" } },
              { value: 0.88, itemStyle: { color: "#849fca" } },
              { value: 0.97, itemStyle: { color: "#849fca" } },
              { value: 0.86, itemStyle: { color: "orange" } },
              { value: 0.84, itemStyle: { color: "#849fca" } },
              { value: 0.98, itemStyle: { color: "#849fca" } },
              { value: 0.99, itemStyle: { color: "#849fca" } },
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
  mounted() {
    this.$nextTick(() => {
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
    });
  },
  methods: {},
  beforeDestroy() {},
};
</script>

<style lang="less" scoped>
.wrapper {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.show1 {
  position: absolute;
  top: 130px;
  left: 100px;
  width: 1271px;
  height: 460px;
  border: 1px solid rgb(2, 40, 120);
}
.BarChart1 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 0px;
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
  top: 0px;
  left: 240px;
  background-color: rgba(0, 0, 0, 0);
}
.BarChart3 {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  // width: 1200px;
  width: 2000px;
  height: 450px;
  top: 0px;
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
  top: 0px;
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
  top: 0px;
  left: 842px;
  background-color: rgba(0, 0, 0, 0);
}
</style>
