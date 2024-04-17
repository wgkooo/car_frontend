<template>
   <div class="wrapper">
      <div class="header1">
         <el-button class="select1" @click="btn" :style='brandStylefirst'>
            <span>Monthly retail performance</span>
         </el-button>
         <el-button class="select2" @click="btn2"  :style="brandStylesecond">
            <span>Monthly performance metrics</span>
         </el-button>
      </div>
      <div class="allDiscount" v-show="allDiscountShow">
         <div id="allDiscountPieChart" class="allDiscountPieChart"></div>
      </div>
      <div class="allDiscount" v-show="carseriesDiscountShow">
        <div class="title1"><p>{{selectBrandData[0]}}</p></div>
        <div class="title2"><p>{{selectCompetitorsData[0]}}</p></div>
        <div class="title3"><p>{{selectCompetitorsData[1]}}</p></div>
        <div class="metrics"> 
            <el-table :data="tableData" style="width: 100%">
             <el-table-column prop="Service" label="Service" width="120"></el-table-column>
             <el-table-column prop="Environment" label="Environment" width="120"></el-table-column>
            </el-table>
        </div>
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

        carseriesName:'123',

         allDiscountPieCharts: null,
         carseriesDiscountPieCharts:null,
        
        brandStylefirst:'',
        brandStylesecond:'',
         
         allDiscountShow:true,
         carseriesDiscountShow:false,

         allDiscountPieOption: {
        legend: {
          orient: 'horizontal',
          x: '10%',
          y: 'bottom',
          data:[]
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
          show:true,
          type: 'value',
          min:0, // 设置y轴刻度的最小值
          max:5,  // 设置y轴刻度的最大值
          splitNumber:10,  // 设置y轴刻度间隔个数
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
            data: [3.62,3.63,3.63,3.63,3.61,3.59],
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
       tableData: [
           {
            Service: '',
            Environment: '',
          }, 
          {
            Service: '',
            Environment: '',
          },
          {
            Service: '',
            Environment: '',
          },
          ]
      }
   },
   created(){
     this.selectBrandData = this.$route.query.selectBrandData
     this.selectCompetitorsData = this.$route.query.selectCompetitorsData
     this.getBrand1Data()
     this.getBrand2Data()
     this.getBrand3Data()
   },
watch:{
},
   mounted() {
     this.initAllPie()
     this.initCarseriesPie()
},
   methods:{
    initAllPie(){
       this.allDiscountPieCharts = Echarts.init(document.getElementById('allDiscountPieChart'))
       this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
     },
    getBrand1Data(){
      this.axios({
        url:'/api/dealertiyan/getdatas',
        method:'GET',
        params:{brand:this.selectBrandData[0]}
      }).then(resp=>{
          this.allDiscountPieOption.series[0].data=[resp.data.result[0],resp.data.result[1],resp.data.result[2],resp.data.result[3],resp.data.result[4],resp.data.result[5]]
          this.allDiscountPieOption.legend.data[0] = this.selectBrandData[0]
          this.allDiscountPieOption.series[0].name = this.selectBrandData[0]

          this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
          //更新metrics
          this.tableData[0].Service = resp.data.result[6]
          this.tableData[0].Environment = resp.data.result[7]
      })
    },
    getBrand2Data(){
      this.axios({
        url:'/api/dealertiyan/getdatas',
        method:'GET',
        params:{brand:this.selectCompetitorsData[0]}
      }).then(resp=>{
          this.allDiscountPieOption.series[1].data=[resp.data.result[0],resp.data.result[1],resp.data.result[2],resp.data.result[3],resp.data.result[4],resp.data.result[5]]
          this.allDiscountPieOption.legend.data[1] = this.selectCompetitorsData[0]
          this.allDiscountPieOption.series[1].name = this.selectCompetitorsData[0]

          this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
          //更新metrics
          this.tableData[1].Service = resp.data.result[6]
          this.tableData[1].Environment = resp.data.result[7]
      })
    },
    getBrand3Data(){
      this.axios({
        url:'/api/dealertiyan/getdatas',
        method:'GET',
        params:{brand:this.selectCompetitorsData[1]}
      }).then(resp=>{
          this.allDiscountPieOption.series[2].data=[resp.data.result[0],resp.data.result[1],resp.data.result[2],resp.data.result[3],resp.data.result[4],resp.data.result[5]]
          this.allDiscountPieOption.legend.data[2] = this.selectCompetitorsData[1]
          this.allDiscountPieOption.series[2].name = this.selectCompetitorsData[1]

          this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
          //更新metrics
          this.tableData[2].Service = resp.data.result[6]
          this.tableData[2].Environment = resp.data.result[7]
      })
    },
    btn(){
      this.allDiscountPieCharts.setOption(this.allDiscountPieOption)
      this.brandStylefirst = 'background-color: rgb(2, 40, 121);color:#FFF;'
      this.brandStylesecond = 'background-color: #FFF;color:rgb(94, 137, 194);'
      this.allDiscountShow = true
      this.carseriesDiscountShow = false
    },
    btn2(){
        this.brandStylefirst = 'background-color: #FFF;color:rgb(94, 137, 194);'
        this.brandStylesecond = 'background-color: rgb(2, 40, 121);color:#FFF;'
        this.allDiscountShow = false
        this.carseriesDiscountShow = true
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
      width:600px;
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
      // background-color: rgb(2, 40, 121);
      background-color: #FFF;
      color:rgb(94, 137, 194);
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
.metrics{
    position: absolute;
    top: 80px;
    left: 400px;
}
.title1{
    background-color: rgb(94, 137, 194);
    width: 80px;
    height: 50px;
    position: absolute;
    top: 150px;
    left: 300px;
    text-align: center;
    color: #fff;
}
.title2{
    background-color: rgb(94, 137, 194);
    width: 80px;
    height: 50px;
    position: absolute;
    top: 222px;
    left: 300px;
    text-align: center;
    color: #fff;
}
.title3{
    background-color: rgb(94, 137, 194);
    width: 80px;
    height: 50px;
    position: absolute;
    top: 290px;
    left: 300px;
    text-align: center;
    color: #fff;
}
/deep/.el-table__row{
    height: 70px;
}
/deep/.cell{
    color: #000;
}
</style>