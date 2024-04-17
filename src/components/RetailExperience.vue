<template>
   <div class="wrapper">
      <div class="select">
         <el-button plain class="selectBrandClass" :style="selectBrandStyle" @click="selectBrandButton">
           <span class="selectBrandContentClass">SELECT BRAND</span>
         </el-button>

         <el-button plain class="selectCompetitorsClass" :style="selectCompetitorsStyle" @click="selectCompetitorsButton">
           <span class="selectCompetitorsContentClass">SELECT COMPETITORS</span>
         </el-button>
      </div>

      <div class="selectBrandShowClass" v-show="selectBrandShow">
      <el-checkbox-group v-model="selectBrandData" :max="1"> 
        <el-checkbox label="Skoda"><img class="img" src="../assets/images/sikeda.png"></el-checkbox>
        <el-checkbox label="SVW"><img class="img" src="../assets/images/shangqi.png"></el-checkbox>
        <el-checkbox label="FAW-VW"><img class="img" src="../assets/images/yiqi.png"></el-checkbox>
    </el-checkbox-group>
    </div>

     <div class="selectCompetitorsShowClass" v-show="selectCompetitorsShow">
       <el-checkbox-group v-model="selectCompetitorsData" :max="2"> 
        <el-checkbox label="Skoda" v-show="selectBrandData!='Skoda'"><img class="img" src="../assets/images/sikeda.png"></el-checkbox>
        <el-checkbox label="SVW" v-show="selectBrandData!='SVW'"><img class="img" src="../assets/images/shangqi.png"></el-checkbox>
        <el-checkbox label="FAW-VW" v-show="selectBrandData!='FAW-VW'"><img class="img" src="../assets/images/yiqi.png"></el-checkbox>
    </el-checkbox-group>
    </div>

    <el-button class="showButtonClass" @click="btn">
      <span>SHOW RESULTS</span>
    </el-button>
   </div>
</template>
<script>
export default {
   data(){
      return{
         selectBrandStyle:'',
         selectCompetitorsStyle:'',

         selectBrandData:[],
         selectCompetitorsData:[],

         selectBrandShow:true,
         selectCompetitorsShow:false,
      }
   },
   watch:{
      selectBrandData(newvalue,old){
         if(this.selectBrandData!=''){
            this.selectBrandStyle = 'background-color:rgb(51,136,255)'
         }
         if(this.selectBrandData==''){
            this.selectBrandStyle = 'background-color:rgb(255,255,255)'
         }
      },
      selectCompetitorsData(newvalue,old){
         if(this.selectCompetitorsData!=''){
            this.selectCompetitorsStyle = 'background-color:rgb(51,136,255)'
         }
         if(this.selectCompetitorsData==''){
            this.selectCompetitorsStyle = 'background-color:rgb(255,255,255)'
         }
      },
       
   },
   methods:{
      selectBrandButton(){
         this.selectBrandShow = true;
         this.selectCompetitorsShow = false;
         this.selectCompetitorsData = []
      },
      selectCompetitorsButton(){
         this.selectBrandShow = false;
         this.selectCompetitorsShow = true;
         this.selectCompetitorsData = []
      },
      btn(){
         if(this.selectBrandData==''){
            alert('please select brand')
         }else if(this.selectCompetitorsData==''){
            alert('please select competitors')
         }else{
            this.$router.push({path:'/retailExperienceDetail',query:{selectBrandData:this.selectBrandData,selectCompetitorsData:this.selectCompetitorsData}})
         }
      },
   }
}
</script>
<style lang="less" scoped>
   .wrapper{
      background-color:rgb(255, 255, 255);
      height: 100%;
   }
   .select{
      position: absolute;
      border: 1px solid rgb(2,40,120);
      top: 200px;
      left: 280px;
      width: 300px;
      height: 300px;
   }
   .selectBrandClass{
      position: absolute;
      top: 30px;
      left: 16px;
      width: 269px;
      height: 100px;
      border:solid 1px rgb(2,40,120);
      border-radius: 0px;
   }
    .selectBrandContentClass{
      color: rgb(2, 40, 120);
   }
   .selectCompetitorsClass{
      position: absolute;
      bottom: 30px;
      left: 6px;
      width: 269px;
      height: 100px;
      border:solid 1px rgb(2,40,120);
      border-radius: 0px;
   }
    .selectCompetitorsContentClass{
      color: rgb(2, 40, 120);
   }
   .selectBrandShowClass{
      position: absolute;
      top: 200px;
      left: 600px;
      // width: 515px;
      // height: 400px;
      border: 1px solid rgb(2,40,120);
      width: 42%;
      height: 450px;
   }
   .img{
      width: 60%;
   }
   .el-checkbox-group{
  overflow: scroll;
  height: 100%;
}
.el-checkbox{
  width: 26%;
   margin-left: 1%;
   margin-top: 2%;
   margin-bottom: 1%;
}
/deep/.el-checkbox__input{
  visibility: hidden;
  float: left;
}
/deep/.el-checkbox__label{
 width: 100%;
   padding-top: 10%;
   padding-bottom: 10%;
   
  color: #606266;
//   font-size: 20px;
//   white-space: normal;
//   padding-left: 0px;
  border: 1px solid  rgb(2,40,120);
}
/deep/.is-checked{
  :last-child{
    background-color: #409EFF;
  }
}
/deep/.el-checkbox__input.is-checked+.el-checkbox__label{
  color: #ffffff;
}
/deep/.el-checkbox__label{
   line-height:28px;
}
.selectCompetitorsShowClass{
      position: absolute;
      top: 200px;
      left: 600px;
      // width: 515px;
      // height: 400px;
      border: 1px solid rgb(2,40,120);
      width: 42%;
      // height: 60%;
      height: 450px;
   }

   .showButtonClass{
      position: absolute;
      top: 560px;
      left: 280px;
      height: 92px;
      width: 302px;
      font-size: 20px;
      color: rgb(2, 40, 120);
      border: 1px solid rgb(2, 40, 120);
      border-radius: 0px;
   }
</style>