<template>
   <div class="wrapper">
      <div class="header1" :style="brandStyle">
         <el-button class="select1" @click="btn" :style='brandStylefirst'>
            <span>Monthly discounts</span>
         </el-button>
         <el-button class="select2" v-show="carseriesShow" :style="carseriesStyle">
            <span>{{carseriesName}}</span>
         </el-button>
      </div>
      <div class="allDiscount" v-show="allDiscountShow">
         <div id="allDiscountPieChart" class="allDiscountPieChart"></div>
      </div>
      <div class="allDiscount" v-show="carseriesDiscountShow">
         <div id="carseriesDiscountPieChart" class="allDiscountPieChart"></div>
      </div>
   </div>
</template>
<script>
import Echarts from 'echarts'

export default {
   data(){
      return{
        selectBrandData:[],
        selectCompetitorsData:[],

        brand1Datas:[],
        brand2Datas:[],
        brand3Datas:[],

        brandStyle:'',
        carseriesName:'123',
        brandStylefirst:'',

         allDiscountPieCharts: null,
         carseriesDiscountPieCharts:null,
        

         carseriesShow:false,
         carseriesStyle:'',
         
         allDiscountShow:true,
         carseriesDiscountShow:false,

         allDiscountPieOption: {
        legend: {
          orient: 'horizontal',
          x: '10%',
          y: 'bottom',
        },
        grid: {
            show:false,
            top: '10%',   // 等价于 y: '16%'
            left: '10%', 
            right: '8%',
            bottom: '10%',
            width:'1000',
            height:'auto',
            containLabel: true,
        },
         xAxis: {
          type: 'category',
          nameLocation:'start',
          axisLine: {
            lineStyle: {
              color: 'black'
            }
          },
           // 设置X轴数据旋转倾斜
          axisLabel: {
            rotate: 0, // 旋转角度
            interval: 0  //设置X轴数据间隔几个显示一个，为0表示都显示
            },
          boundaryGap: false,
          data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul','Aug','Sep','Oct','Nov','Dec']
        },
        yAxis: {
           show:false,
          type: 'value',
          min:0, // 设置y轴刻度的最小值
          max:30,  // 设置y轴刻度的最大值
          splitNumber:12,  // 设置y轴刻度间隔个数
          axisLine: {
            // show:false,
            lineStyle: {
              // 设置y轴颜色
              color: '#87CEFA'
            }
          },
        },
         series: [
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(231,104,17)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
 
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(76,116,181)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(177,200,230',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
        ],
        color: ['rgb(231,104,17)', 'rgb(76,116,181)','rgb(177,200,230)']
      },
      carseriesDiscountPieOption: {
           title: {
        },
        legend: {
          // orient 设置布局方式，默认水平布局，可选值：'horizontal'（水平） ¦ 'vertical'（垂直）
          orient: 'horizontal',
          // x 设置水平安放位置，默认全图居中，可选值：'center' ¦ 'left' ¦ 'right' ¦ {number}（x坐标，单位px）
          x: '10%',
          // y 设置垂直安放位置，默认全图顶端，可选值：'top' ¦ 'bottom' ¦ 'center' ¦ {number}（y坐标，单位px）
          y: 'bottom',
        },
         //  图表距边框的距离,可选值：'百分比'¦ {number}（单位px）
        grid: {
            show:false,
            top: '10%',   // 等价于 y: '16%'
            left: '10%', 
            right: '8%',
            bottom: '10%',
            width:'1000',
            height:'auto',
            containLabel: true,
        },
          toolbox: {
            feature: {
               //  saveAsImage: {} //下载工具
            }
        },
         xAxis: {
         //  name: '月份',
          type: 'category',
          nameLocation:'start',
          axisLine: {
            lineStyle: {
              // 设置x轴颜色
              color: 'black'
            }
          },
           // 设置X轴数据旋转倾斜
          axisLabel: {
            rotate: 0, // 旋转角度
            interval: 0  //设置X轴数据间隔几个显示一个，为0表示都显示
            },
          // boundaryGap值为false的时候，折线第一个点在y轴上
          boundaryGap: false,
          data: []
        },
        yAxis: {
           show:false,
         //  name: 'Monthly discounts',
          type: 'value',
          min:0, // 设置y轴刻度的最小值
          max:30,  // 设置y轴刻度的最大值
          splitNumber:12,  // 设置y轴刻度间隔个数
          axisLine: {
            // show:false,
            lineStyle: {
              // 设置y轴颜色
              color: '#87CEFA'
            }
          },
        },
         series: [
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
 
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(76,116,181)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(135,163,207)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
         
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(177,200,230',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
         
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(196,199,200)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'dashed'  //'dotted'虚线 'solid'实线
                }
              }
            }
         
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(138,140,142)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'dotted'  //'dotted'虚线 'solid'实线
                }
              }
            }
         
          },
          {
            name: '',
            data: [],
            type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
         
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
          {
            name: '',
            data: [],
           type: 'line',
            // 设置折线上圆点大小
            symbol: 'none',
             // 设置拐点为实心圆
            symbol:'circle',  
            smooth:false, //关键点，为true是不支持虚线的，默认值为实线(true)
            itemStyle:{
              normal:{
                // 拐点上显示数值
                label : {
                show: true
                },
                borderColor:'rgb(2,40,121)',  // 拐点边框颜色
                lineStyle:{                 
                  width:2,  // 设置线宽
                  type:'solid'  //'dotted'虚线 'solid'实线
                }
              }
            }
          },
        ],
        color: ['rgb(2,40,121)', 'rgb(76,116,181)','rgb(135,163,207)','rgb(177,200,230)','rgb(196,199,200)','rgb(138,140,142)','rgb(2,40,121)']
      },
      }
   },
   created(){
     this.selectBrandData = this.$route.query.selectBrandData
     this.selectCompetitorsData = this.$route.query.selectCompetitorsData
    // 请求每个品牌的数据
    this.getBrandData(this.selectBrandData[0], 1)
    this.getBrandData(this.selectCompetitorsData[0], 2)
    this.getBrandData(this.selectCompetitorsData[1], 3)
   },
   mounted() {
    // 初始化折线图
     this.allDiscountPieCharts = Echarts.init(document.getElementById('allDiscountPieChart'))
     this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
     // 设置折线图的点击事件
     this.allDiscountPieCharts.on('click',(params)=>{
         this.brandStyle = 'width:600px;'
         this.brandStylefirst = 'background-color:#fff;color:rgb(76,116,181);'
         this.allDiscountShow = false,
         this.carseriesDiscountShow = true
         this.carseriesShow = true

         //设置header的carseriesName
        this.carseriesName = params.seriesName

        //设置carseriesDiscountPieOption的数据
        for (let i = 0;i<13;i++){
          this.carseriesDiscountPieOption['series'][i]['data'] = []
          this.carseriesDiscountPieOption['series'][i]['name'] = name
        }
        this.carseriesDiscountPieCharts.setOption(this.carseriesDiscountPieOption)
        this.getCarseriesData(params.seriesName)
     })
     // 初始化折线图
     this.carseriesDiscountPieCharts = Echarts.init(document.getElementById('carseriesDiscountPieChart'))
     this.carseriesDiscountPieCharts.setOption(this.carseriesDiscountPieOption)
},
methods:{
        getBrandData(brand,type){
            this.axios({
                url:'/api/discount/selectByBrandYearMonth',
                method:'POST',
                params:{brand: brand}
                }).then(resp=>{
                    if(type == 1){
                        //设置月份
                        this.allDiscountPieOption.xAxis.data = [resp.data.result[11].englishbuymonth,resp.data.result[10].englishbuymonth,resp.data.result[9].englishbuymonth,resp.data.result[8].englishbuymonth,resp.data.result[7].englishbuymonth,resp.data.result[6].englishbuymonth,resp.data.result[5].englishbuymonth,resp.data.result[4].englishbuymonth,resp.data.result[3].englishbuymonth,resp.data.result[2].englishbuymonth,resp.data.result[1].englishbuymonth,resp.data.result[0].englishbuymonth]
                        //设置车标名字
                        // this.allDiscountPieOption['series'][0]['name'] = resp.data.result[0]['brand']
                        this.allDiscountPieOption['series'][0]['name'] = resp.data.result[0].englishBrand
                        //设置对应月份的数据
                        this.allDiscountPieOption['series'][0]['data'] = [resp.data.result[11].discount,resp.data.result[10].discount,resp.data.result[9].discount,resp.data.result[8].discount,resp.data.result[7].discount,resp.data.result[6].discount,resp.data.result[5].discount,resp.data.result[4].discount,resp.data.result[3].discount,resp.data.result[2].discount,resp.data.result[1].discount,resp.data.result[0].discount,]
        this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
                    }else if(type == 2){
                        //设置车标名字
                        // this.allDiscountPieOption['series'][1]['name'] = resp.data.result[0]['brand']
                        this.allDiscountPieOption['series'][1]['name'] = resp.data.result[0].englishBrand
                        //设置对应月份的数据
                        this.allDiscountPieOption['series'][1]['data'] = [resp.data.result[11].discount,resp.data.result[10].discount,resp.data.result[9].discount,resp.data.result[8].discount,resp.data.result[7].discount,resp.data.result[6].discount,resp.data.result[5].discount,resp.data.result[4].discount,resp.data.result[3].discount,resp.data.result[2].discount,resp.data.result[1].discount,resp.data.result[0].discount,]
        this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
                    }else if(type == 3){
                        //设置车标名字
                        // this.allDiscountPieOption['series'][2]['name'] = resp.data.result[0]['brand']
                        this.allDiscountPieOption['series'][2]['name'] = resp.data.result[0].englishBrand
                        //设置对应月份的数据
                        this.allDiscountPieOption['series'][2]['data'] = [resp.data.result[11].discount,resp.data.result[10].discount,resp.data.result[9].discount,resp.data.result[8].discount,resp.data.result[7].discount,resp.data.result[6].discount,resp.data.result[5].discount,resp.data.result[4].discount,resp.data.result[3].discount,resp.data.result[2].discount,resp.data.result[1].discount,resp.data.result[0].discount,]
        this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
                    }
                })
                },
        getCarseriesData(brand){
            //向后端发送数据请求
            this.axios({
                url:'/api/discount/selectAllCarseriesByBrand',
                method:'POST',
                params:{brand:brand}
      }).then(resp=>{
        //清空series的数据
        for(let i=0;i<13;i++){
          this.carseriesDiscountPieOption.series[i].data = []
        }
        //设置月份
          this.carseriesDiscountPieOption.xAxis.data = [resp.data[0][11].englishbuymonth,resp.data[0][10].englishbuymonth,resp.data[0][9].englishbuymonth,resp.data[0][8].englishbuymonth,resp.data[0][7].englishbuymonth,resp.data[0][6].englishbuymonth,resp.data[0][5].englishbuymonth,resp.data[0][4].englishbuymonth,resp.data[0][3].englishbuymonth,resp.data[0][2].englishbuymonth,resp.data[0][1].englishbuymonth,resp.data[0][0].englishbuymonth,]

        for(let i=0;i<resp.data.length;i++){
          this.carseriesDiscountPieOption.series[i].name = resp.data[i][0].carseries
          //设置每月的数据
          this.carseriesDiscountPieOption.series[i].data = [resp.data[i][11].discount,resp.data[i][10].discount,resp.data[i][9].discount,resp.data[i][8].discount,resp.data[i][7].discount,resp.data[i][6].discount,resp.data[i][5].discount,resp.data[i][4].discount,resp.data[i][3].discount,resp.data[i][2].discount,resp.data[i][1].discount,resp.data[i][0].discount,]
        }
        this.carseriesDiscountPieCharts.setOption(this.carseriesDiscountPieOption)

      })
        },

       btn(){
      this.allDiscountShow = true
      this.carseriesDiscountShow = false
      this.carseriesShow = false
      this.brandStyle = 'width:300px;'
      this.brandStylefirst = 'background-color:rgb(2, 40, 121);color:#fff;'
    },
   },
}
</script>
<style lang="less" scoped>
   .allDiscount{
      position: absolute;
      top: 130px;
      left: 100px;
      width: 1271px;
      height: 450px;
      border: 1px solid rgb(2,40,120);
   }
   .header1{
      position: absolute;
      top: 90px;
      left: 100px;
      // width: 530px;
      width:300px;
      height: 40px;
      border: 1px solid rgb(2,40,120);
      border-bottom: none;
   }
   .select1{
      position: absolute;
      top: 0px;
      left: 0px;
      width: 300px;
      height: 40px;
      border-radius: 0px;
      background-color: rgb(2, 40, 121);
      color:#FFF;
      // color: rgb(76,116,181);
   }
   .select2{
      position: absolute;
      top: 0px;
      left: 291px;
      width: 300px;
      height: 40px;
      border-radius: 0px;
      // background-color: rgb(2, 40, 121);
       background-color: rgb(2, 40, 121);
      color:#FFF;
   }
   
   .allDiscountPieChart {
  border-radius: 4px;
  background: #fff;
  position: absolute;
  width: 1200px;
  height: 400px;
  top: 0px;
  left: 0px;
  background-color:rgba(0,0,0,0);
}
.img1{
   position: absolute;
   height: 14%;
   top: 180px;
   left: 140px;
}
</style>