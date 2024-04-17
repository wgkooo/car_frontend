<template>
  <div class="wrapper">
     <br><br><br><br><br><br>
     <el-row>
        <el-col :offset="7">
        <el-button icon="el-icon-download" @click="linkButton">download</el-button>
        </el-col>
     </el-row>
    <div class="select">
      <el-button plain class="button1" :style="button1class" @click="button1">
        <span class="sp">SELECT BRAND</span>
      </el-button>

      <span class="span2">PORTFOLIO</span>

      <el-button plain class="button3" @click="button3" :style="button2class1">
        <span class="span33">COMPARE</span>
        <span class="span33">PORTFOLIO</span>
      </el-button>

      <el-button plain class="button4" @click="button4" :style="button2class2">
        <span class="sp1">COMPARE</span>
        <span class="sp1">BY MODEL</span>
      </el-button>

      <span class="span5">COMPETITION</span>
      <el-button plain class="button6" :style="button3class1" @click="button8">
        <span class="sp1">AUTO-SELECT</span>
        <span class="sp1">COMPETITORS</span>
      </el-button>
      <el-button plain class="button7" @click="button7" :style="button3class2">
        <span class="sp1">SELECT</span>
        <span class="sp1">COMPETITORS</span>
      </el-button>
    </div>

    <div class="show1" v-show="show1">
      <el-checkbox-group v-model="select1" :max="1">
        <el-checkbox label="MERCEDES_BENZ"
          ><img class="img" src="../assets/images/benchi.png"
        /></el-checkbox>
        <el-checkbox label="BMW"
          ><img class="img" src="../assets/images/baoma.png"
        /></el-checkbox>
        <el-checkbox label="AUDI"
          ><img class="img" src="../assets/images/aodi.png"
        /></el-checkbox>
        <el-checkbox label="CADILLAC"
          ><img class="img" src="../assets/images/kaidilake.png"
        /></el-checkbox>
        <el-checkbox label="LAND_ROVER"
          ><img class="img" src="../assets/images/luhu.png"
        /></el-checkbox>
        <el-checkbox label="SAIC_VOLKSWAGEN"
          ><img class="img" src="../assets/images/shangqi.png"
        /></el-checkbox>
        <el-checkbox label="FAW_VOLKSWAGEN"
          ><img class="img" src="../assets/images/yiqi.png"
        /></el-checkbox>
        <el-checkbox label="NIO"
          ><img class="img" src="../assets/images/nio.png"
        /></el-checkbox>
        <el-checkbox label="WELTMEISTER"
          ><img class="img" src="../assets/images/weima.png"
        /></el-checkbox>
        <el-checkbox label="XPENG"
          ><img class="img" src="../assets/images/xiaopeng.png"
        /></el-checkbox>
        <el-checkbox label="LI_AUTO"
          ><img class="img" src="../assets/images/lixiang.png"
        /></el-checkbox>
        <el-checkbox label="BYD"
          ><img class="img" src="../assets/images/byd.png"
        /></el-checkbox>

        <el-checkbox label="PORSCHE"
          ><img class="img" src="../assets/images/baoshijie.png"
        /></el-checkbox>
        <el-checkbox label="BENTLEY"
          ><img class="img" src="../assets/images/binli.png"
        /></el-checkbox>
        <el-checkbox label="ASTON_MARTIN"
          ><img class="img" src="../assets/images/martin.png"
        /></el-checkbox>
        <el-checkbox label="LAMBORGHINI"
          ><img class="img" src="../assets/images/lanbojini.png"
        /></el-checkbox>
        <el-checkbox label="MCLAREN"
          ><img class="img" src="../assets/images/mkl.png"
        /></el-checkbox>
        <el-checkbox label="ROLLS_ROYCE"
          ><img class="img" src="../assets/images/RR.png"
        /></el-checkbox>
        <el-checkbox label="FERRARI"
          ><img class="img" src="../assets/images/falali.png"
        /></el-checkbox>

        <el-checkbox label="SKODA"
          ><img class="img" src="../assets/images/sikeda.png"
        /></el-checkbox>
        <el-checkbox label="PEUGEOT"
          ><img class="img" src="../assets/images/biaozhi.png"
        /></el-checkbox>
        <el-checkbox label="CITROEN"
          ><img class="img" src="../assets/images/xuetielong.png"
        /></el-checkbox>
        <el-checkbox label="TESLA"
          ><img class="img" src="../assets/images/tsl.png"
        /></el-checkbox>

        <el-checkbox label="HYUNDAI"
          ><img class="img" src="../assets/images/hyundai.png"
        /></el-checkbox>
        <el-checkbox label="KIA"
          ><img class="img" src="../assets/images/kia.png"
        /></el-checkbox>

        <el-checkbox label="HONGQI"
          ><img class="img" src="../assets/images/hongqi.png"
        /></el-checkbox>
        <el-checkbox label="HIPHI"
          ><img class="img" src="../assets/images/hiphi.png"
        /></el-checkbox>

        <el-checkbox label="ORA"
          ><img class="img" src="../assets/images/ora.png"
        /></el-checkbox>
        <el-checkbox label="TOYOTA"
          ><img class="img" src="../assets/images/toyota.png"
        /></el-checkbox>
        <el-checkbox label="WULING"
          ><img class="img" src="../assets/images/wuling.png"
        /></el-checkbox>
        <el-checkbox label="AION"
          ><img class="img" src="../assets/images/aion.png"
        /></el-checkbox>
        <el-checkbox label="HOVER"
          ><img class="img" src="../assets/images/hover.png"
        /></el-checkbox>
        <el-checkbox label="HONDA"
          ><img class="img" src="../assets/images/honda.png"
        /></el-checkbox>
        <el-checkbox label="VOLVO"
          ><img class="img" src="../assets/images/volvo.png"
        /></el-checkbox>
      </el-checkbox-group>
    </div>

    <div class="show2" v-show="show2">
      <el-checkbox-group v-model="select2" :max="1">
        <el-checkbox :label="item.name" v-for="(item, i) in carmodel" :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
      </el-checkbox-group>
    </div>

    <div class="show3" v-show="show33">
      <el-checkbox-group v-model="select3" :max="2">
        <el-checkbox label="MERCEDES_BENZ" v-show="select1 != 'MERCEDES_BENZ'"
          ><img class="img" src="../assets/images/benchi.png"
        /></el-checkbox>
        <el-checkbox label="BMW" v-show="select1 != 'BMW'"
          ><img class="img" src="../assets/images/baoma.png"
        /></el-checkbox>
        <el-checkbox label="AUDI" v-show="select1 != 'AUDI'"
          ><img class="img" src="../assets/images/aodi.png"
        /></el-checkbox>
        <el-checkbox label="CADILLAC" v-show="select1 != 'CADILLAC'"
          ><img class="img" src="../assets/images/kaidilake.png"
        /></el-checkbox>
        <el-checkbox label="LAND_ROVER" v-show="select1 != 'LAND_ROVER'"
          ><img class="img" src="../assets/images/luhu.png"
        /></el-checkbox>
        <el-checkbox
          label="SAIC_VOLKSWAGEN"
          v-show="select1 != 'SAIC_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/shangqi.png"
        /></el-checkbox>
        <el-checkbox label="FAW_VOLKSWAGEN" v-show="select1 != 'FAW_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/yiqi.png"
        /></el-checkbox>
        <el-checkbox label="NIO" v-show="select1 != 'NIO'"
          ><img class="img" src="../assets/images/nio.png"
        /></el-checkbox>
        <el-checkbox label="WELTMEISTER" v-show="select1 != 'WELTMEISTER'"
          ><img class="img" src="../assets/images/weima.png"
        /></el-checkbox>
        <el-checkbox label="XPENG" v-show="select1 != 'XPENG'"
          ><img class="img" src="../assets/images/xiaopeng.png"
        /></el-checkbox>
        <el-checkbox label="LI_AUTO" v-show="select1 != 'LI_AUTO'"
          ><img class="img" src="../assets/images/lixiang.png"
        /></el-checkbox>
        <el-checkbox label="BYD" v-show="select1 != 'BYD'"
          ><img class="img" src="../assets/images/byd.png"
        /></el-checkbox>

        <el-checkbox label="PORSCHE" v-show="select1 != 'PORSCHE'"
          ><img class="img" src="../assets/images/baoshijie.png"
        /></el-checkbox>
        <el-checkbox label="BENTLEY" v-show="select1 != 'BENTLEY'"
          ><img class="img" src="../assets/images/binli.png"
        /></el-checkbox>
        <el-checkbox label="ASTON_MARTIN" v-show="select1 != 'ASTON_MARTIN'"
          ><img class="img" src="../assets/images/martin.png"
        /></el-checkbox>
        <el-checkbox label="LAMBORGHINI" v-show="select1 != 'LAMBORGHINI'"
          ><img class="img" src="../assets/images/lanbojini.png"
        /></el-checkbox>
        <el-checkbox label="MCLAREN" v-show="select1 != 'MCLAREN'"
          ><img class="img" src="../assets/images/mkl.png"
        /></el-checkbox>
        <el-checkbox label="ROLLS_ROYCE" v-show="select1 != 'ROLLS_ROYCE'"
          ><img class="img" src="../assets/images/RR.png"
        /></el-checkbox>
        <el-checkbox label="FERRARI" v-show="select1 != 'FERRARI'"
          ><img class="img" src="../assets/images/falali.png"
        /></el-checkbox>

        <el-checkbox label="SKODA" v-show="select1 != 'SKODA'"
          ><img class="img" src="../assets/images/sikeda.png"
        /></el-checkbox>
        <el-checkbox label="PEUGEOT" v-show="select1 != 'PEUGEOT'"
          ><img class="img" src="../assets/images/biaozhi.png"
        /></el-checkbox>
        <el-checkbox label="CITROEN" v-show="select1 != 'CITROEN'"
          ><img class="img" src="../assets/images/xuetielong.png"
        /></el-checkbox>
        <el-checkbox label="TESLA" v-show="select1 != 'TESLA'"
          ><img class="img" src="../assets/images/tsl.png"
        /></el-checkbox>

        <el-checkbox label="HYUNDAI" v-show="select1 != 'HYUNDAI'"
          ><img class="img" src="../assets/images/hyundai.png"
        /></el-checkbox>
        <el-checkbox label="kia" v-show="select1 != 'kia'"
          ><img class="img" src="../assets/images/kia.png"
        /></el-checkbox>

        <el-checkbox label="HONGQI" v-show="select1 != 'HONGQI'"
          ><img class="img" src="../assets/images/hongqi.png"
        /></el-checkbox>
        <el-checkbox label="HIPHI" v-show="select1 != 'HIPHI'"
          ><img class="img" src="../assets/images/hiphi.png"
        /></el-checkbox>

        <el-checkbox label="ORA" v-show="select1 != 'ORA'"
          ><img class="img" src="../assets/images/ora.png"
        /></el-checkbox>
        <el-checkbox label="TOYOTA" v-show="select1 != 'TOYOTA'"
          ><img class="img" src="../assets/images/toyota.png"
        /></el-checkbox>
        <el-checkbox label="WULING" v-show="select1 != 'WULING'"
          ><img class="img" src="../assets/images/wuling.png"
        /></el-checkbox>
        <el-checkbox label="AION" v-show="select1 != 'AION'"
          ><img class="img" src="../assets/images/aion.png"
        /></el-checkbox>
        <el-checkbox label="HOVER" v-show="select1 != 'HOVER'"
          ><img class="img" src="../assets/images/hover.png"
        /></el-checkbox>
        <el-checkbox label="HONDA" v-show="select1 != 'HONDA'"
          ><img class="img" src="../assets/images/honda.png"
        /></el-checkbox>
        <el-checkbox label="VOLVO" v-show="select1 != 'VOLVO'"
          ><img class="img" src="../assets/images/volvo.png"
        /></el-checkbox>
      </el-checkbox-group>
    </div>

    <div class="show3" v-show="show31">
      <el-checkbox-group v-model="select3" :max="2">
        <el-checkbox
          :label="item"
          v-for="(item, i) in select31data"
          :key="i"
          ><span class="select1span">{{ item }}</span></el-checkbox
        >
      </el-checkbox-group>
    </div>

    <div class="show3" v-show="show2131">
      <el-checkbox-group v-model="select3" :max="2">
        <el-checkbox label="MERCEDES_BENZ" v-show="select1 != 'MERCEDES_BENZ'"
          ><img class="img" src="../assets/images/benchi.png"
        /></el-checkbox>
        <el-checkbox label="BMW" v-show="select1 != 'BMW'"
          ><img class="img" src="../assets/images/baoma.png"
        /></el-checkbox>
        <el-checkbox label="AUDI" v-show="select1 != 'AUDI'"
          ><img class="img" src="../assets/images/aodi.png"
        /></el-checkbox>
        <el-checkbox label="CADILLAC" v-show="select1 != 'CADILLAC'"
          ><img class="img" src="../assets/images/kaidilake.png"
        /></el-checkbox>
        <el-checkbox label="LAND_ROVER" v-show="select1 != 'LAND_ROVER'"
          ><img class="img" src="../assets/images/luhu.png"
        /></el-checkbox>
        <el-checkbox
          label="SAIC_VOLKSWAGEN"
          v-show="select1 != 'SAIC_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/shangqi.png"
        /></el-checkbox>
        <el-checkbox label="FAW_VOLKSWAGEN" v-show="select1 != 'FAW_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/yiqi.png"
        /></el-checkbox>
        <el-checkbox label="NIO" v-show="select1 != 'NIO'"
          ><img class="img" src="../assets/images/nio.png"
        /></el-checkbox>
        <el-checkbox label="WELTMEISTER" v-show="select1 != 'WELTMEISTER'"
          ><img class="img" src="../assets/images/weima.png"
        /></el-checkbox>
        <el-checkbox label="XPENG" v-show="select1 != 'XPENG'"
          ><img class="img" src="../assets/images/xiaopeng.png"
        /></el-checkbox>
        <el-checkbox label="LI_AUTO" v-show="select1 != 'LI_AUTO'"
          ><img class="img" src="../assets/images/lixiang.png"
        /></el-checkbox>
        <el-checkbox label="BYD" v-show="select1 != 'BYD'"
          ><img class="img" src="../assets/images/byd.png"
        /></el-checkbox>

        <el-checkbox label="PORSCHE" v-show="select1 != 'PORSCHE'"
          ><img class="img" src="../assets/images/baoshijie.png"
        /></el-checkbox>
        <el-checkbox label="BENTLEY" v-show="select1 != 'BENTLEY'"
          ><img class="img" src="../assets/images/binli.png"
        /></el-checkbox>
        <el-checkbox label="ASTON_MARTIN" v-show="select1 != 'ASTON_MARTIN'"
          ><img class="img" src="../assets/images/martin.png"
        /></el-checkbox>
        <el-checkbox label="LAMBORGHINI" v-show="select1 != 'LAMBORGHINI'"
          ><img class="img" src="../assets/images/lanbojini.png"
        /></el-checkbox>
        <el-checkbox label="MCLAREN" v-show="select1 != 'MCLAREN'"
          ><img class="img" src="../assets/images/mkl.png"
        /></el-checkbox>
        <el-checkbox label="ROLLS_ROYCE" v-show="select1 != 'ROLLS_ROYCE'"
          ><img class="img" src="../assets/images/RR.png"
        /></el-checkbox>
        <el-checkbox label="FERRARI" v-show="select1 != 'FERRARI'"
          ><img class="img" src="../assets/images/falali.png"
        /></el-checkbox>

        <el-checkbox label="SKODA" v-show="select1 != 'SKODA'"
          ><img class="img" src="../assets/images/sikeda.png"
        /></el-checkbox>
        <el-checkbox label="PEUGEOT" v-show="select1 != 'PEUGEOT'"
          ><img class="img" src="../assets/images/biaozhi.png"
        /></el-checkbox>
        <el-checkbox label="CITROEN" v-show="select1 != 'CITROEN'"
          ><img class="img" src="../assets/images/xuetielong.png"
        /></el-checkbox>
        <el-checkbox label="TESLA" v-show="select1 != 'TESLA'"
          ><img class="img" src="../assets/images/tsl.png"
        /></el-checkbox>

        <el-checkbox label="HYUNDAI" v-show="select1 != 'HYUNDAI'"
          ><img class="img" src="../assets/images/hyundai.png"
        /></el-checkbox>
        <el-checkbox label="KIA" v-show="select1 != 'KIA'"
          ><img class="img" src="../assets/images/kia.png"
        /></el-checkbox>

        <el-checkbox label="HONGQI" v-show="select1 != 'HONGQI'"
          ><img class="img" src="../assets/images/hongqi.png"
        /></el-checkbox>
        <el-checkbox label="HIPHI" v-show="select1 != 'HIPHI'"
          ><img class="img" src="../assets/images/hiphi.png"
        /></el-checkbox>

        <el-checkbox label="ORA" v-show="select1 != 'ORA'"
          ><img class="img" src="../assets/images/ora.png"
        /></el-checkbox>
        <el-checkbox label="TOYOTA" v-show="select1 != 'TOYOTA'"
          ><img class="img" src="../assets/images/toyota.png"
        /></el-checkbox>
        <el-checkbox label="WULING" v-show="select1 != 'WULING'"
          ><img class="img" src="../assets/images/wuling.png"
        /></el-checkbox>
        <el-checkbox label="AION" v-show="select1 != 'AION'"
          ><img class="img" src="../assets/images/aion.png"
        /></el-checkbox>
        <el-checkbox label="HOVER" v-show="select1 != 'HOVER'"
          ><img class="img" src="../assets/images/hover.png"
        /></el-checkbox>
        <el-checkbox label="HONDA" v-show="select1 != 'HONDA'"
          ><img class="img" src="../assets/images/honda.png"
        /></el-checkbox>
        <el-checkbox label="VOLVO" v-show="select1 != 'VOLVO'"
          ><img class="img" src="../assets/images/volvo.png"
        /></el-checkbox>
      </el-checkbox-group>
    </div>

    <div class="show3" v-show="show3">
      <el-checkbox-group v-model="select3" :max="1">
        <el-checkbox
          label="MERCEDES_BENZ"
          disabled=""
          v-show="select1 != 'MERCEDES_BENZ'"
          ><img class="img" src="../assets/images/benchi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'MERCEDES_BENZ'"
          v-for="(item, i) in benchi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="BMW" disabled="" v-show="select1 != 'BMW'"
          ><img class="img" src="../assets/images/baoma.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'BMW'"
          v-for="(item, i) in baoma"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="AUDI" disabled="" v-show="select1 != 'AUDI'"
          ><img class="img" src="../assets/images/aodi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'AUDI'"
          v-for="(item, i) in aodi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="CADILLAC" disabled="" v-show="select1 != 'CADILLAC'"
          ><img class="img" src="../assets/images/kaidilake.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'CADILLAC'"
          v-for="(item, i) in kaidilake"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox
          label="LAND_ROVER"
          disabled=""
          v-show="select1 != 'LAND_ROVER'"
          ><img class="img" src="../assets/images/luhu.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'LAND_ROVER'"
          v-for="(item, i) in luhu"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="SAIC_VOLKSWAGEN"
          disabled=""
          v-show="select1 != 'SAIC_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/shangqi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'SAIC_VOLKSWAGEN'"
          v-for="(item, i) in shangqi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="FAW_VOLKSWAGEN"
          disabled=""
          v-show="select1 != 'FAW_VOLKSWAGEN'"
          ><img class="img" src="../assets/images/yiqi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'FAW_VOLKSWAGEN'"
          v-for="(item, i) in yiqi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="NIO" disabled="" v-show="select1 != 'NIO'"
          ><img class="img" src="../assets/images/nio.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'NIO'"
          v-for="(item, i) in nio"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="WELTMEISTER"
          disabled=""
          v-show="select1 != 'WELTMEISTER'"
          ><img class="img" src="../assets/images/weima.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'WELTMEISTER'"
          v-for="(item, i) in weima"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="XPENG" disabled="" v-show="select1 != 'XPENG'"
          ><img class="img" src="../assets/images/xiaopeng.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'XPENG'"
          v-for="(item, i) in xiaopeng"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="LI_AUTO" disabled="" v-show="select1 != 'LI_AUTO'"
          ><img class="img" src="../assets/images/lixiang.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'LI_AUTO'"
          v-for="(item, i) in lixiang"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="BYD" disabled="" v-show="select1 != 'BYD'"
          ><img class="img" src="../assets/images/byd.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'BYD'"
          v-for="(item, i) in byd"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="PORSCHE" disabled="" v-show="select1 != 'PORSCHE'"
          ><img class="img" src="../assets/images/baoshijie.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'PORSCHE'"
          v-for="(item, i) in baoshijie"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="BENTLEY" disabled="" v-show="select1 != 'BENTLEY'"
          ><img class="img" src="../assets/images/binli.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'BENTLEY'"
          v-for="(item, i) in binli"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="ASTON_MARTIN"
          disabled=""
          v-show="select1 != 'ASTON_MARTIN'"
          ><img class="img" src="../assets/images/martin.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'ASTON_MARTIN'"
          v-for="(item, i) in martin"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="LAMBORGHINI"
          disabled=""
          v-show="select1 != 'LAMBORGHINI'"
          ><img class="img" src="../assets/images/lanbojini.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'LAMBORGHINI'"
          v-for="(item, i) in lanbojini"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="MCLAREN" disabled="" v-show="select1 != 'MCLAREN'"
          ><img class="img" src="../assets/images/mkl.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'MCLAREN'"
          v-for="(item, i) in mkl"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox
          label="ROLLS_ROYCE"
          disabled=""
          v-show="select1 != 'ROLLS_ROYCE'"
          ><img class="img" src="../assets/images/RR.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'ROLLS_ROYCE'"
          v-for="(item, i) in rr"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="FERRARI" disabled="" v-show="select1 != 'FERRARI'"
          ><img class="img" src="../assets/images/falali.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'FERRARI'"
          v-for="(item, i) in falali"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="SKODA" disabled="" v-show="select1 != 'SKODA'"
          ><img class="img" src="../assets/images/sikeda.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'SKODA'"
          v-for="(item, i) in sikeda"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="PEUGEOT" disabled="" v-show="select1 != 'PEUGEOT'"
          ><img class="img" src="../assets/images/biaozhi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'PEUGEOT'"
          v-for="(item, i) in biaozhi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="CITROEN" disabled="" v-show="select1 != 'CITROEN'"
          ><img class="img" src="../assets/images/xuetielong.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'CITROEN'"
          v-for="(item, i) in xuetielong"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="TESLA" disabled="" v-show="select1 != 'TESLA'"
          ><img class="img" src="../assets/images/tsl.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'TESLA'"
          v-for="(item, i) in tesla"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="HYUNDAI" disabled="" v-show="select1 != 'HYUNDAI'"
          ><img class="img" src="../assets/images/hyundai.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'HYUNDAI'"
          v-for="(item, i) in hyundai"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="KIA" disabled="" v-show="select1 != 'KIA'"
          ><img class="img" src="../assets/images/kia.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'KIA'"
          v-for="(item, i) in kia"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="HONGQI" disabled="" v-show="select1 != 'HONGQI'"
          ><img class="img" src="../assets/images/hongqi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'HONGQI'"
          v-for="(item, i) in hongqi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="HIPHI" disabled="" v-show="select1 != 'HIPHI'"
          ><img class="img" src="../assets/images/hiphi.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'HIPHI'"
          v-for="(item, i) in hiphi"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >

        <el-checkbox label="ORA" disabled="" v-show="select1 != 'ORA'"
          ><img class="img" src="../assets/images/ora.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'ORA'"
          v-for="(item, i) in ora"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="TOYOTA" disabled="" v-show="select1 != 'TOYOTA'"
          ><img class="img" src="../assets/images/toyota.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'TOYOTA'"
          v-for="(item, i) in toyota"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="WULING" disabled="" v-show="select1 != 'WULING'"
          ><img class="img" src="../assets/images/wuling.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'WULING'"
          v-for="(item, i) in wuling"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="AION" disabled="" v-show="select1 != 'AION'"
          ><img class="img" src="../assets/images/aion.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'AION'"
          v-for="(item, i) in aion"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="HOVER" disabled="" v-show="select1 != 'HOVER'"
          ><img class="img" src="../assets/images/hover.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'HOVER'"
          v-for="(item, i) in hover"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="HONDA" disabled="" v-show="select1 != 'HONDA'"
          ><img class="img" src="../assets/images/honda.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'HONDA'"
          v-for="(item, i) in honda"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
        <el-checkbox label="VOLVO" disabled="" v-show="select1 != 'VOLVO'"
          ><img class="img" src="../assets/images/volvo.png"
        /></el-checkbox>
        <el-checkbox
          :label="item.name"
          v-show="select1 != 'VOLVO'"
          v-for="(item, i) in volvo"
          :key="i"
          ><span class="select1span">{{ item.name }}</span></el-checkbox
        >
      </el-checkbox-group>
    </div>
    <el-button class="show" @click="btn">
      <span class="span9">SHOW RESULTS</span>
    </el-button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      select1: [],
      select2: [],
      select3: [],

      button1class: "",
      button2class1: "",
      button2class2: "",
      button3class1: "",
      button3class2: "",

      select22: [],
      select33: [],
      show1: true,
      show2: false,
      show22: false,
      show3: false,
      show33: false,
      show31: false,
      show2131: false,
      brand: [],
      select31data: [],
      select2131data: [],
      carmodel: [
        {
          id: 1,
          brand: "奥迪",
          model: "奥迪A4L  2020款 35 TFSI 时尚动感型",
        },
        {
          id: 2,
          brand: "奥迪",
          model: "奥迪A4L  2020款 40 TFSI 时尚动感型",
        },
        {
          id: 3,
          brand: "奥迪",
          model: "奥迪A4L  2020款 40 TFSI 时尚致雅型",
        },

        {
          id: 4,
          brand: "奥迪",
          model: "奥迪A4L  2020款 40 TFSI 豪华动感型",
        },
        {
          id: 5,
          brand: "奥迪",
          model: "宝马",
        },
        {
          id: 6,
          brand: "奥迪",
          model: "奥迪A4L  2020款 40 发发放松房贷首付方法撒发撒",
        },
      ],
      benchi: [],
      baoma: [],
      aodi: [],
      kaidilake: [],
      luhu: [],
      shangqi: [],
      yiqi: [],
      nio: [],
      weima: [],
      xiaopeng: [],
      lixiang: [],
      byd: [],
      baoshijie: [],
      binli: [],
      martin: [],
      lanbojini: [],
      mkl: [],
      rr: [],
      falali: [],
      sikeda: [],
      biaozhi: [],
      xuetielong: [],
      tesla: [],
      hyundai: [],
      kia: [],
      hongqi: [],
      hiphi: [],
      ora: [],
      toyota: [],
      wuling: [],
      aion: [],
      hover: [],
      honda: [],
      volvo: [],
    };
  },
  watch: {
    select1(newvalue, old) {
      if (this.select1 != "") {
        this.button1class = "background-color:rgb(51,136,255)";
      }
      if (this.select1 == "") {
        this.button1class = "background-color:rgb(255,255,255)";
      }
    },
    show22(newvalue, old) {
      if (this.show22 == true) {
        this.button2class1 = "background-color:rgb(51,136,255)";
        this.button2class2 = "background-color:rgb(255,255,255)";
      }
      if (this.show22 == false) {
        this.button2class1 = "background-color:rgb(255,255,255)";
      }
    },
    select2(newvalue, old) {
      if (this.show22 == false && this.select2 != "") {
        this.button2class2 = "background-color:rgb(51,136,255)";
      }
      if (this.show22 == false && this.select2 == "") {
        this.button2class2 = "background-color:rgb(255,255,255)";
      }
    },
    show31(newvalue, old) {
      if (this.show31 == true) {
        this.button3class1 = "background-color:rgb(51,136,255)";
        this.button3class2 = "background-color:rgb(255,255,255)";
      }
      if (this.show31 == false) {
        this.button3class1 = "background-color:rgb(255,255,255)";
        this.button3class2 = "background-color:rgb(255,255,255)";
      }
    },
    select3(newvalue, old) {
      if (this.select3 != "" && this.show3 == true) {
        this.button3class1 = "background-color:rgb(255,255,255)";
        this.button3class2 = "background-color:rgb(51,136,255)";
      }
      if (this.select3 != "" && this.show33 == true) {
        this.button3class1 = "background-color:rgb(255,255,255)";
        this.button3class2 = "background-color:rgb(51,136,255)";
      }
      if (this.select3 != "" && this.show2131 == true) {
        this.button3class1 = "background-color:rgb(51,136,255)";
        this.button3class2 = "background-color:rgb(255,255,255)";
      }
      if (this.select3 == "") {
        this.button3class1 = "background-color:rgb(255,255,255)";
        this.button3class2 = "background-color:rgb(255,255,255)";
      }
    },
  },
  methods: {
    button1() {
      this.show1 = true;
      this.show2 = false;
      this.show3 = false;
      this.show33 = false;
      this.show31 = false;
      this.show2131 = false;
      this.select2 = [];
      htis.select3 = [];
    },
    button3() {
      if (this.show22 == true) {
        this.show1 = false;
        this.show2 = true;
        this.show22 = false;
        this.show3 = false;
        this.show33 = false;
        this.show31 = false;
        this.show2131 = false;
      }
      if (this.show22 == false) {
        this.show1 = true;
        this.show2 = false;
        this.show22 = true;
        this.show3 = false;
        this.show33 = false;
        this.show31 = false;
        this.show2131 = false;

        this.select2 = [];
        this.select3 = [];
      }
    },
    button4() {
      this.show1 = false;
      this.show2 = true;
      this.show22 = false;
      this.show3 = false;
      this.show33 = false;
      this.show31 = false;
      this.show2131 = false;
      this.select3 = [];

      this.axios({
        url: "/api/koubei/queryCarAllModel",
        methods: "POST",
        params: {
          brand: this.select1[0],
        },
      })  
        .then((resp) => {
          console.log(resp)
          this.carmodel = resp.data.result;
          this.select2 = [];
        })
        .catch((error) => {
          // alert("查询失败");
        });
    },
    button7() {
      if (this.show2 == true) {
        this.show1 = false;
        this.show2 = false;
        this.show22 = false;
        this.show3 = true;
        this.show33 = false;
        this.show31 = false;
        this.show2131 = false;
        this.select3 = [];
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "MERCEDES_BENZ",
          },
        }).then((resp) => {
          this.benchi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "BMW",
          },
        }).then((resp) => {
          this.baoma = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "AUDI",
          },
        }).then((resp) => {
          this.aodi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "CADILLAC",
          },
        }).then((resp) => {
          this.kaidilake = resp.data.result;
        });

        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "LAND_ROVER",
          },
        }).then((resp) => {
          this.luhu = rresp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "SAIC_VOLKSWAGEN",
          },
        }).then((resp) => {
          this.shangqi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "FAW_VOLKSWAGEN",
          },
        }).then((resp) => {
          this.yiqi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "NIO",
          },
        }).then((resp) => {
          this.nio = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "WELTMEISTER",
          },
        }).then((resp) => {
          this.weima = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "XPENG",
          },
        }).then((resp) => {
          this.xiaopeng = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "LI_AUTO",
          },
        }).then((resp) => {
          this.lixiang = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "BYD",
          },
        }).then((resp) => {
          this.byd = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "PORSCHE",
          },
        }).then((resp) => {
          this.baoshijie = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "BENTLEY",
          },
        }).then((resp) => {
          this.binli = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "ASTON_MARTIN",
          },
        }).then((resp) => {
          this.martin = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "LAMBORGHINI",
          },
        }).then((resp) => {
          this.lanbojini = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "MCLAREN",
          },
        }).then((resp) => {
          this.mkl = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "ROLLS_ROYCE",
          },
        }).then((resp) => {
          this.rr = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "FERRARI",
          },
        }).then((resp) => {
          this.falali = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "SKODA",
          },
        }).then((resp) => {
          this.sikeda = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "PEUGEOT",
          },
        }).then((resp) => {
          this.biaozhi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "CITROEN",
          },
        }).then((resp) => {
          this.xuetielong = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "TESLA",
          },
        }).then((resp) => {
          this.tesla = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "HYUNDAI",
          },
        }).then((resp) => {
          this.hyundai = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "KIA",
          },
        }).then((resp) => {
          this.kia = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "HONGQI",
          },
        }).then((resp) => {
          this.hongqi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "HIPHI",
          },
        }).then((resp) => {
          this.hiphi = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "ORA",
          },
        }).then((resp) => {
          this.ora = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "TOYOTA",
          },
        }).then((resp) => {
          this.toyota = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "WULING",
          },
        }).then((resp) => {
          this.wuling = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "AION",
          },
        }).then((resp) => {
          this.aion = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "HOVER",
          },
        }).then((resp) => {
          this.hover = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "HONDA",
          },
        }).then((resp) => {
          this.honda = resp.data.result;
        });
        this.axios({
          url: "/api/koubei/queryCarAllModel",
          method: 'GET',
          params: {
            brand: "VOLVO",
          },
        }).then((resp) => {
          this.volvo = resp.data.result;
        });
      }
      if (this.show22 == true) {
        this.show1 = false;
        this.show2 = false;
        // this.show22 = false;
        this.show3 = false;
        this.show2131 = false;
        this.show33 = true;
        this.select3 = [];
      }
    },
    button8() {
      console.log('show2:')
      console.log(this.show2)
      console.log('show22:')
      console.log(this.show22)
      if (this.show2 == false) {
        this.show1 = false;
        this.show2 = false;
        // this.show22 = false;
        this.show3 = false;
        this.show33 = false;
        this.show31 = false;
        this.show2131 = true;
        this.axios({
          url: "/api/koubei/autoSelectByBrand",
          methods: "POST",
          params: { brand: this.select1[0] },
          // params:{brand:'奔驰'}
        }).then((resp) => {
          this.select3 = [];
          this.select31data = [];
          for (let index = 0; index < resp.data.result.length; index++) {
            if (resp.data.result[index].brand != this.select2[0]) {
              this.select3.push(resp.data.result[index].brand);
              this.select2131data.push(resp.data.result[index]);
            }
          }
          console.log(this.select3)
          console.log(this.select2131data)
        });
      }

      if (this.show22 == false) {
        this.show1 = false;
        this.show2 = false;
        this.show22 = false;
        this.show3 = false;
        this.show33 = false;
        this.show31 = true;
        this.show2131 = false;
        this.axios({
          url: "/api/koubei/autoSelectByModel",
          methods: "POST",
          params: { name: this.select2[0] },
        }).then((resp) => {
          this.select3 = [];
          this.select31data = [];
          // for (let index = 0; index < resp.data.result.length; index++) {
          for (let index = 0; index < 1; index++) {
            if (resp.data.result[index].brand != this.select2[0]) {
              // this.select3.push(resp.data.result[index].brand);
              this.select3.push(resp.data.result[index].name);
              this.select31data.push(resp.data.result[index].name);
            }
          }
          console.log(this.select3)
          console.log(this.select31data)
        });
      }
    },
    btn() {
      if (this.show3 == true) {
        if (this.select1.length != 1) {
          alert("Please select brand");
        } else if (this.select2.length != 1) {
          alert("Please select compare by model");
        } else if (this.select3.length == 0) {
          alert("Please select competitors");
        } else {
          this.$router.push({
            path: "/productEvaluationByCarModel",
            query: {
              select1: this.select1,
              select2: this.select2,
              select3: this.select3,
            },
          });
        }
      }
      if (this.show33 == true) {
        this.$router.push({
          path: "/productEvaluationByCarBrand",
          query: {
            select1: this.select1,
            select2: this.select1,
            select3: this.select3,
          },
        });
        // this.$router.push({path:'/test',query:{select1:this.select1,select2:this.select1,select3:this.select3}})
      }
      if (this.show31 == true) {
        this.$router.push({
          path: "/productEvaluationByCarModel",
          query: {
            select1: this.select1,
            select2: this.select2,
            select3: this.select3,
          },
        });
        // this.$router.push({path:'/test2',query:{select1:this.select1,select2:this.select2,select3:this.select3}})
      }
      if (this.show2131 == true) {
        this.$router.push({
          path: "/productEvaluationByCarBrand",
          query: {
            select1: this.select1,
            select2: this.select1,
            select3: this.select3,
          },
        });
        // this.$router.push({path:'/test',query:{select1:this.select1,select2:this.select1,select3:this.select3}})
      }
    },
    linkButton() {
       this.$router.push({
          path: "/easyExcel",
       })
    }
  },
};
</script>
<style lang="less" scoped>
.wrapper {
  background-color: rgb(255, 255, 255);
  height: 100%;
}
.select {
  position: absolute;
  border: 1px solid rgb(2, 40, 120);
  top: 200px;
  left: 280px;
  width: 300px;
  height: 300px;
}
.show1 {
  position: absolute;
  top: 200px;
  left: 600px;
  // width: 515px;
  // height: 400px;
  border: 1px solid rgb(2, 40, 120);
  width: 42%;
  height: 450px;
}
.show2 {
  position: absolute;
  top: 200px;
  left: 600px;
  // width: 515px;
  // height: 400px;
  border: 1px solid rgb(2, 40, 120);
  width: 42%;
  height: 450px;
}
.show3 {
  position: absolute;
  top: 200px;
  left: 600px;
  // width: 515px;
  // height: 400px;
  border: 1px solid rgb(2, 40, 120);
  width: 42%;
  height: 450px;
}
.button1 {
  position: absolute;
  top: 16px;
  left: 16px;
  width: 269px;
  height: 40px;
  border: solid 1px rgb(2, 40, 120);
  border-radius: 0px;
}
.span1 {
  color: grey;
}
.sp {
  color: rgb(2, 40, 120);
}
.span2 {
  position: absolute;
  color: rgbw(2, 40, 120);
  top: 80px;
  left: 16px;
  font-size: 20px;
}
.button3 {
  position: absolute;
  top: 110px;
  left: 16px;
  width: 125px;
  height: 50px;
  border: solid 1px rgb(2, 40, 120);
  border-radius: 0px;
}
.span3 {
  font-size: 12px;
  display: block;
}
.span33 {
  font-size: 12px;
  display: block;
  color: rgb(2, 40, 120);
}
.sp1 {
  font-size: 12px;
  display: block;
  color: rgb(2, 40, 120);
}
.button4 {
  position: absolute;
  top: 110px;
  right: 16px;
  width: 125px;
  height: 50px;
  border: solid 1px rgb(2, 40, 120);
  border-radius: 0px;
}
.span4 {
  font-size: 12px;
  display: block;
}
.span5 {
  position: absolute;
  color: rgb(2, 40, 120);
  top: 180px;
  left: 16px;
  font-size: 20px;
}
.button6 {
  position: absolute;
  top: 210px;
  left: 16px;
  width: 125px;
  height: 50px;
  border: solid 1px rgb(2, 40, 120);
  border-radius: 0px;
}
.span6 {
  font-size: 12px;
  display: block;
}
.button7 {
  position: absolute;
  top: 210px;
  right: 16px;
  width: 125px;
  height: 50px;
  border: solid 1px rgb(2, 40, 120);
  border-radius: 0px;
}
.span7 {
  font-size: 12px;
  display: block;
}

.show {
  position: absolute;
  top: 560px;
  left: 280px;
  height: 92px;
  width: 300px;
  font-size: 20px;
  color: rgb(2, 40, 120);
  border: 1px solid rgb(2, 40, 120);
  border-radius: 0px;
}

.el-checkbox-group {
  overflow: scroll;
  height: 100%;
}
.el-checkbox {
  width: 26%;
  margin-left: 1%;
  margin-top: 2%;
  margin-bottom: 1%;
}
/deep/.el-checkbox__input {
  visibility: hidden;
  float: left;
}
/deep/.el-checkbox__label {
  width: 100%;
  padding-top: 10%;
  padding-bottom: 10%;
  color: #606266;
  border: 1px solid rgb(2, 40, 120);
}
/deep/.is-checked {
  :last-child {
    background-color: #409eff;
  }
}
/deep/.el-checkbox__input.is-checked + .el-checkbox__label {
  color: #ffffff;
}
.img {
  width: 60%;
}
.select1span {
  display: block;
  padding-top: 50%;
}
/deep/.el-checkbox__label {
  line-height: 28px;
}
</style>