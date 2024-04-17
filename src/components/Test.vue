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
      <div class="list">
        <span class="spanList" v-for="item in propertyList" :key="item">{{
          item
        }}</span>
      </div>

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

      <div class="list1" :style="list1style">
        <!-- <el-progress :text-inside="true" :stroke-width="20" v-for="item in brand1Datas" :key="item" :percentage="item*10" class="progress2"></el-progress> -->
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="overallColor1"
          :stroke-width="20"
          :percentage="brand1Datas.overall * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="exteriorColor1"
          :stroke-width="20"
          :percentage="brand1Datas.exterior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="interiorColor1"
          :stroke-width="20"
          :percentage="brand1Datas.interior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="carspaceColor1"
          :stroke-width="20"
          :percentage="brand1Datas.carspace * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="valueformoneyColor1"
          :stroke-width="20"
          :percentage="brand1Datas.valueformoney * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="powerColor1"
          :stroke-width="20"
          :percentage="brand1Datas.power * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="maneuverabilityColor1"
          :stroke-width="20"
          :percentage="brand1Datas.maneuverability * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="fuelconsumptionColor1"
          :stroke-width="20"
          :percentage="brand1Datas.fuelconsumption * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="comfortColor1"
          :stroke-width="20"
          :percentage="brand1Datas.comfort * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="optionsandfeaturesColor1"
          :stroke-width="20"
          :percentage="brand1Datas.optionsandfeatures * 50"
          class="progress2"
        ></el-progress>
      </div>
      <div class="list11">
        <!-- <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.exterior}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.interior}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.carspace}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.optionsortrim}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.power}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.maneuverability}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.fuelconsumption}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand1Datas.comfort}}</span> -->

        <span class="list11Span">{{ brand1Datas.overall }}</span>
        <span class="list11Span">{{ brand1Datas.exterior }}</span>
        <span class="list11Span">{{ brand1Datas.interior }}</span>
        <span class="list11Span">{{ brand1Datas.carspace }}</span>
        <span class="list11Span">{{ brand1Datas.valueformoney }}</span>
        <span class="list11Span">{{ brand1Datas.power }}</span>
        <span class="list11Span">{{ brand1Datas.maneuverability }}</span>
        <span class="list11Span">{{ brand1Datas.fuelconsumption }}</span>
        <span class="list11Span">{{ brand1Datas.comfort }}</span>
        <span class="list11Span">{{ brand1Datas.optionsandfeatures }}</span>
      </div>

      <div class="list2" :style="list2style">
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="overallColor2"
          :percentage="brand2Datas.overall * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="exteriorColor2"
          :percentage="brand2Datas.exterior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="interiorColor2"
          :percentage="brand2Datas.interior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="carspaceColor2"
          :percentage="brand2Datas.carspace * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="valueformoneyColor2"
          :percentage="brand2Datas.valueformoney * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="powerColor2"
          :percentage="brand2Datas.power * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="maneuverabilityColor2"
          :percentage="brand2Datas.maneuverability * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="fuelconsumptionColor2"
          :percentage="brand2Datas.fuelconsumption * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="comfortColor2"
          :percentage="brand2Datas.comfort * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="optionsandfeaturesColor2"
          :percentage="brand2Datas.optionsandfeatures * 50"
          class="progress2"
        ></el-progress>
      </div>
      <div class="list22" v-show="brand2datasShow">
        <!-- <span class="list11Span">{{brand2Datas.exterior}}</span>
             <span class="list11Span">{{brand2Datas.interior}}</span>
             <span class="list11Span">{{brand2Datas.carspace}}</span>
             <span class="list11Span">{{brand2Datas.optionsortrim}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand2Datas.power}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand2Datas.maneuverability}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand2Datas.fuelconsumption}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand2Datas.comfort}}</span> -->

        <span class="list11Span">{{ brand2Datas.overall }}</span>
        <span class="list11Span">{{ brand2Datas.exterior }}</span>
        <span class="list11Span">{{ brand2Datas.interior }}</span>
        <span class="list11Span">{{ brand2Datas.carspace }}</span>
        <span class="list11Span">{{ brand2Datas.valueformoney }}</span>
        <span class="list11Span">{{ brand2Datas.power }}</span>
        <span class="list11Span">{{ brand2Datas.maneuverability }}</span>
        <span class="list11Span">{{ brand2Datas.fuelconsumption }}</span>
        <span class="list11Span">{{ brand2Datas.comfort }}</span>
        <span class="list11Span">{{ brand2Datas.optionsandfeatures }}</span>
      </div>

      <div class="list3" :style="list3style">
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="overallColor3"
          :percentage="brand3Datas.overall * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="exteriorColor3"
          :percentage="brand3Datas.exterior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="interiorColor3"
          :percentage="brand3Datas.interior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="carspaceColor3"
          :percentage="brand3Datas.carspace * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="valueformoneyColor3"
          :percentage="brand3Datas.valueformoney * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="powerColor3"
          :percentage="brand3Datas.power * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="maneuverabilityColor3"
          :percentage="brand3Datas.maneuverability * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="fuelconsumptionColor3"
          :percentage="brand3Datas.fuelconsumption * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="comfortColor3"
          :percentage="brand3Datas.comfort * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="optionsandfeaturesColor3"
          :percentage="brand3Datas.optionsandfeatures * 50"
          class="progress2"
        ></el-progress>
      </div>
      <div class="list33" v-show="brand3datasShow">
        <!-- <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.exterior}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.interior}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.carspace}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.optionsortrim}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.power}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.maneuverability}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.fuelconsumption}}</span>
             <span class="list11Span" v-for="item in brand1Datas" :key="item">{{brand3Datas.comfort}}</span> -->

        <span class="list11Span">{{ brand3Datas.overall }}</span>
        <span class="list11Span">{{ brand3Datas.exterior }}</span>
        <span class="list11Span">{{ brand3Datas.interior }}</span>
        <span class="list11Span">{{ brand3Datas.carspace }}</span>
        <span class="list11Span">{{ brand3Datas.valueformoney }}</span>
        <span class="list11Span">{{ brand3Datas.power }}</span>
        <span class="list11Span">{{ brand3Datas.maneuverability }}</span>
        <span class="list11Span">{{ brand3Datas.fuelconsumption }}</span>
        <span class="list11Span">{{ brand3Datas.comfort }}</span>
        <span class="list11Span">{{ brand3Datas.optionsandfeatures }}</span>
      </div>
      <div class="list4" :style="list4style">
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="overallColor4"
          :percentage="brand4Datas.overall * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="exteriorColor4"
          :percentage="brand4Datas.exterior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="interiorColor4"
          :percentage="brand4Datas.interior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="carspaceColor4"
          :percentage="brand4Datas.carspace * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="valueformoneyColor4"
          :percentage="brand4Datas.valueformoney * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="powerColor4"
          :percentage="brand4Datas.power * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="maneuverabilityColor4"
          :percentage="brand4Datas.maneuverability * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="fuelconsumptionColor4"
          :percentage="brand4Datas.fuelconsumption * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="comfortColor4"
          :percentage="brand4Datas.comfort * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :stroke-width="20"
          :color="optionsandfeaturesColor4"
          :percentage="brand4Datas.optionsandfeatures * 50"
          class="progress2"
        ></el-progress>
      </div>
      <div class="list44" v-show="brand4datasShow">
        <span class="list11Span">{{ brand4Datas.overall }}</span>
        <span class="list11Span">{{ brand4Datas.exterior }}</span>
        <span class="list11Span">{{ brand4Datas.interior }}</span>
        <span class="list11Span">{{ brand4Datas.carspace }}</span>
        <span class="list11Span">{{ brand4Datas.valueformoney }}</span>
        <span class="list11Span">{{ brand4Datas.power }}</span>
        <span class="list11Span">{{ brand4Datas.maneuverability }}</span>
        <span class="list11Span">{{ brand4Datas.fuelconsumption }}</span>
        <span class="list11Span">{{ brand4Datas.comfort }}</span>
        <span class="list11Span">{{ brand4Datas.optionsandfeatures }}</span>
      </div>
      <div class="list5" :style="list5style">
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="overallColor5"
          :stroke-width="20"
          :percentage="brand5Datas.overall * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="exteriorColor5"
          :stroke-width="20"
          :percentage="brand5Datas.exterior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="interiorColor5"
          :stroke-width="20"
          :percentage="brand5Datas.interior * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="carspaceColor5"
          :stroke-width="20"
          :percentage="brand5Datas.carspace * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="valueformoneyColor5"
          :stroke-width="20"
          :percentage="brand5Datas.valueformoney * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="powerColor5"
          :stroke-width="20"
          :percentage="brand5Datas.power * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="maneuverabilityColor5"
          :stroke-width="20"
          :percentage="brand5Datas.maneuverability * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="fuelconsumptionColor5"
          :stroke-width="20"
          :percentage="brand5Datas.fuelconsumption * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="comfortColor5"
          :stroke-width="20"
          :percentage="brand5Datas.comfort * 50"
          class="progress2"
        ></el-progress>
        <el-progress
          :text-inside="true"
          :show-text="false"
          :color="optionsandfeaturesColor5"
          :stroke-width="20"
          :percentage="brand5Datas.optionsandfeatures * 50"
          class="progress2"
        ></el-progress>
      </div>
      <div class="list55" v-show="brand5datasShow">
        <span class="list11Span">{{ brand5Datas.overall }}</span>
        <span class="list11Span">{{ brand5Datas.exterior }}</span>
        <span class="list11Span">{{ brand5Datas.interior }}</span>
        <span class="list11Span">{{ brand5Datas.carspace }}</span>
        <span class="list11Span">{{ brand5Datas.valueformoney }}</span>
        <span class="list11Span">{{ brand5Datas.power }}</span>
        <span class="list11Span">{{ brand5Datas.maneuverability }}</span>
        <span class="list11Span">{{ brand5Datas.fuelconsumption }}</span>
        <span class="list11Span">{{ brand5Datas.comfort }}</span>
        <span class="list11Span">{{ brand5Datas.optionsandfeatures }}</span>
      </div>

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
  </div>
</template>
<script>
import Echarts from "echarts";
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

      // brand1:'Mercedes-BenzS-Class Maybach',
      // brand2:'Rolls-Royce Ghost',
      // brand3:'Bentley Flying Spur',
      propertyList: [
        "Overall",
        "Exterior",
        "Interior",
        "CarSpace",
        "Valueformoney",
        "Power",
        "Maneuverability",
        "Fuelconsumption",
        "Comfort",
        "Optionsandfeatures",
      ],
      brand1Datas: {},
      brand2Datas: {},
      brand3Datas: {},
      brand4Datas: {},
      brand5Datas: {},
      // brand3Datas:[{}],
      // img1:'../assets/images/benchi.png',
      // img2:'../assets/images/benchi.png',
      // img3:'../assets/images/benchi.png',
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

      window.addEventListener("resize", this.handleResize);
    });
  },
  created() {
    this.select1 = this.$route.select1;
    this.select2 = this.$route.query.select2[0];
    this.select3 = this.$route.query.select3;
    console.log(this.select1);
    console.log(this.select2);
    console.log(this.select2.toString());
    console.log(this.select3);

    this.getBrand1Datas();
    this.getBrand2Datas();
    this.getBrand3Datas();
    this.getBrand4Datas();
    this.getBrand5Datas();

    // this.getpiedata(this.select2,this.pieOption,0)
    // if(this.select3[0] != null){
    //    this.getpiedata(this.select3[0],this.pieOption1,1)
    // }

    // if(this.select3[1] != null && (this.select3[1].substring(0,2)!=this.select3[0].substring(0,2))){
    //    this.getpiedata(this.select3[1],this.pieOption2,2)
    // }else if(this.select3[1] != null && this.select3[2]!=null
    // &&(this.select3[2].substring(0,2)!=this.select3[0].substring(0,2)
    // &&this.select3[2].substring(0,2)!=this.select3[1].substring(0,2))){
    //    this.getpiedata(this.select3[2],this.pieOption2,2)
    // }else if(this.select3[1] != null && this.select3[2]!=null && this.select3[3]!= null
    // &&(this.select3[3].substring(0,2)!=this.select3[0].substring(0,2)
    // &&this.select3[3].substring(0,2)!=this.select3[1].substring(0,2)
    // &&this.select3[3].substring(0,2)!=this.select3[2].substring(0,2))){
    //    this.getpiedata(this.select3[3],this.pieOption2,2)
    // }

    this.getdata();
    this.getkoubeNum();
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
      this.koubeiNum =
        this.brand1Num +
        this.brand2Num +
        this.brand3Num +
        this.brand4Num +
        this.brand5Num;
    },
  },
  methods: {
    getpiedata(carbrand, pieOption, pieChartsNum) {
      this.axios({
        url: "/api/piedatas/queryAllcategoryByBrand",
        method: "POST",
        params: { brand: carbrand },
      }).then((resp) => {
        pieOption.title.text = resp.data[0].brand;
        for (let i = 0; i < resp.data.length; i++) {
          //数据赋值
          pieOption.series[0].data[i].value = resp.data[i].categoryrate;
          pieOption.series[0].data[i].name = resp.data[i].category;
          //change color
          if (resp.data[i].commenttype == "正面评论") {
            pieOption.color[i] = "rgb(53,91,183)";
          } else {
            pieOption.color[i] = "rgb(165,184,225)";
          }
        }
        //更新饼图 、 设置车的图标
        if (pieChartsNum == 0) {
          this.pieCharts.setOption(pieOption);
          this.changeCarImg(resp.data[0].brand, 0);
        }
        if (pieChartsNum == 1) {
          this.pieCharts1.setOption(pieOption);
          this.changeCarImg(resp.data[0].brand, 1);
        }
        if (pieChartsNum == 2) {
          this.pieCharts2.setOption(pieOption);
          this.changeCarImg(resp.data[0].brand, 2);
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
    getkoubeNum() {
      this.axios({
        url: "/api/koubei/queryAllNumByDate",
        method: "POST",
        params: { date: this.value },
      }).then((resp) => {
        // this.koubeiNum = resp.data
      });
    },
    getdata() {
      this.axios({
        url: "/api/koubei/querydate",
        method: "POST",
      }).then((resp) => {
        let datalength = resp.data.length;
        this.value = resp.data[datalength - 1].substring(0, 7);
        this.options[0].value = resp.data[datalength - 1];
        this.options[0].label = resp.data[datalength - 1].substring(0, 7);
        for (let index = datalength - 2; index >= 0; index--) {
          this.options.push({
            value: resp.data[index],
            label: resp.data[index].substring(0, 7),
          });
        }
        console.log(this.options);
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
    showBrand1Datas() {
      let brand;
      brand = this.findMax(
        this.brand1Datas.overall,
        this.brand2Datas.overall,
        this.brand3Datas.overall,
        this.brand4Datas.overall,
        this.brand5Datas.overall
      );
      if (brand == "brand1") {
        this.overallColor1 = "orange";
        this.overallColor2 = "#849fca";
        this.overallColor3 = "#849fca";
        this.overallColor4 = "#849fca";
        this.overallColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.overallColor1 = "#849fca";
        this.overallColor2 = "orange";
        this.overallColor3 = "#849fca";
        this.overallColor4 = "#849fca";
        this.overallColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.overallColor1 = "#849fca";
        this.overallColor2 = "#849fca";
        this.overallColor3 = "orange";
        this.overallColor4 = "#849fca";
        this.overallColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.overallColor1 = "#849fca";
        this.overallColor2 = "#849fca";
        this.overallColor3 = "#849fca";
        this.overallColor4 = "orange";
        this.overallColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.overallColor1 = "#849fca";
        this.overallColor2 = "#849fca";
        this.overallColor3 = "#849fca";
        this.overallColor4 = "#849fca";
        this.overallColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.exterior,
        this.brand2Datas.exterior,
        this.brand3Datas.exterior,
        this.brand4Datas.exterior,
        this.brand5Datas.exterior
      );
      if (brand == "brand1") {
        this.exteriorColor1 = "orange";
        this.exteriorColor2 = "#849fca";
        this.exteriorColor3 = "#849fca";
        this.exteriorColor4 = "#849fca";
        this.exteriorColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.exteriorColor1 = "#849fca";
        this.exteriorColor2 = "orange";
        this.exteriorColor3 = "#849fca";
        this.exteriorColor4 = "#849fca";
        this.exteriorColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.exteriorColor1 = "#849fca";
        this.exteriorColor2 = "#849fca";
        this.exteriorColor3 = "orange";
        this.exteriorColor4 = "#849fca";
        this.exteriorColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.exteriorColor1 = "#849fca";
        this.exteriorColor2 = "#849fca";
        this.exteriorColor3 = "#849fca";
        this.exteriorColor4 = "orange";
        this.exteriorColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.exteriorColor1 = "#849fca";
        this.exteriorColor2 = "#849fca";
        this.exteriorColor3 = "#849fca";
        this.exteriorColor4 = "#849fca";
        this.exteriorColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.interior,
        this.brand2Datas.interior,
        this.brand3Datas.interior,
        this.brand4Datas.interior,
        this.brand5Datas.interior
      );
      if (brand == "brand1") {
        this.interiorColor1 = "orange";
        this.interiorColor2 = "#849fca";
        this.interiorColor3 = "#849fca";
        this.interiorColor4 = "#849fca";
        this.interiorColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.interiorColor1 = "#849fca";
        this.interiorColor2 = "orange";
        this.interiorColor3 = "#849fca";
        this.interiorColor4 = "#849fca";
        this.interiorColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.interiorColor1 = "#849fca";
        this.interiorColor2 = "#849fca";
        this.interiorColor3 = "orange";
        this.interiorColor4 = "#849fca";
        this.interiorColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.interiorColor1 = "#849fca";
        this.interiorColor2 = "#849fca";
        this.interiorColor3 = "#849fca";
        this.interiorColor4 = "orange";
        this.interiorColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.interiorColor1 = "#849fca";
        this.interiorColor2 = "#849fca";
        this.interiorColor3 = "#849fca";
        this.interiorColor4 = "#849fca";
        this.interiorColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.carspace,
        this.brand2Datas.carspace,
        this.brand3Datas.carspace,
        this.brand4Datas.carspace,
        this.brand5Datas.carspace
      );
      if (brand == "brand1") {
        this.carspaceColor1 = "orange";
        this.carspaceColor2 = "#849fca";
        this.carspaceColor3 = "#849fca";
        this.carspaceColor4 = "#849fca";
        this.carspaceColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.carspaceColor1 = "#849fca";
        this.carspaceColor2 = "orange";
        this.carspaceColor3 = "#849fca";
        this.carspaceColor4 = "#849fca";
        this.carspaceColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.carspaceColor1 = "#849fca";
        this.carspaceColor2 = "#849fca";
        this.carspaceColor3 = "orange";
        this.carspaceColor4 = "#849fca";
        this.carspaceColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.carspaceColor1 = "#849fca";
        this.carspaceColor2 = "#849fca";
        this.carspaceColor3 = "#849fca";
        this.carspaceColor4 = "orange";
        this.carspaceColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.carspaceColor1 = "#849fca";
        this.carspaceColor2 = "#849fca";
        this.carspaceColor3 = "#849fca";
        this.carspaceColor4 = "#849fca";
        this.carspaceColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.valueformoney,
        this.brand2Datas.valueformoney,
        this.brand3Datas.valueformoney,
        this.brand4Datas.valueformoney,
        this.brand5Datas.valueformoney
      );
      if (brand == "brand1") {
        this.valueformoneyColor1 = "orange";
        this.valueformoneyColor2 = "#849fca";
        this.valueformoneyColor3 = "#849fca";
        this.valueformoneyColor4 = "#849fca";
        this.valueformoneyColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.valueformoneyColor1 = "#849fca";
        this.valueformoneyColor2 = "orange";
        this.valueformoneyColor3 = "#849fca";
        this.valueformoneyColor4 = "#849fca";
        this.valueformoneyColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.valueformoneyColor1 = "#849fca";
        this.valueformoneyColor2 = "#849fca";
        this.valueformoneyColor3 = "orange";
        this.valueformoneyColor4 = "#849fca";
        this.valueformoneyColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.valueformoneyColor1 = "#849fca";
        this.valueformoneyColor2 = "#849fca";
        this.valueformoneyColor3 = "#849fca";
        this.valueformoneyColor4 = "orange";
        this.valueformoneyColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.valueformoneyColor1 = "#849fca";
        this.valueformoneyColor2 = "#849fca";
        this.valueformoneyColor3 = "#849fca";
        this.valueformoneyColor4 = "#849fca";
        this.valueformoneyColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.power,
        this.brand2Datas.power,
        this.brand3Datas.power,
        this.brand4Datas.power,
        this.brand5Datas.power
      );
      if (brand == "brand1") {
        this.powerColor1 = "orange";
        this.powerColor2 = "#849fca";
        this.powerColor3 = "#849fca";
        this.powerColor4 = "#849fca";
        this.powerColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.powerColor1 = "#849fca";
        this.powerColor2 = "orange";
        this.powerColor3 = "#849fca";
        this.powerColor4 = "#849fca";
        this.powerColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.powerColor1 = "#849fca";
        this.powerColor2 = "#849fca";
        this.powerColor3 = "orange";
        this.powerColor4 = "#849fca";
        this.powerColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.powerColor1 = "#849fca";
        this.powerColor2 = "#849fca";
        this.powerColor3 = "#849fca";
        this.powerColor4 = "orange";
        this.powerColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.powerColor1 = "#849fca";
        this.powerColor2 = "#849fca";
        this.powerColor3 = "#849fca";
        this.powerColor4 = "#849fca";
        this.powerColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.maneuverability,
        this.brand2Datas.maneuverability,
        this.brand3Datas.maneuverability,
        this.brand4Datas.maneuverability,
        this.brand5Datas.maneuverability
      );
      if (brand == "brand1") {
        this.maneuverabilityColor1 = "orange";
        this.maneuverabilityColor2 = "#849fca";
        this.maneuverabilityColor3 = "#849fca";
        this.maneuverabilityColor4 = "#849fca";
        this.maneuverabilityColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.maneuverabilityColor1 = "#849fca";
        this.maneuverabilityColor2 = "orange";
        this.maneuverabilityColor3 = "#849fca";
        this.maneuverabilityColor4 = "#849fca";
        this.maneuverabilityColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.maneuverabilityColor1 = "#849fca";
        this.maneuverabilityColor2 = "#849fca";
        this.maneuverabilityColor3 = "orange";
        this.maneuverabilityColor4 = "#849fca";
        this.maneuverabilityColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.maneuverabilityColor1 = "#849fca";
        this.maneuverabilityColor2 = "#849fca";
        this.maneuverabilityColor3 = "#849fca";
        this.maneuverabilityColor4 = "orange";
        this.maneuverabilityColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.maneuverabilityColor1 = "#849fca";
        this.maneuverabilityColor2 = "#849fca";
        this.maneuverabilityColor3 = "#849fca";
        this.maneuverabilityColor4 = "#849fca";
        this.maneuverabilityColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.fuelconsumption,
        this.brand2Datas.fuelconsumption,
        this.brand3Datas.fuelconsumption,
        this.brand4Datas.fuelconsumption,
        this.brand5Datas.fuelconsumption
      );
      if (brand == "brand1") {
        this.fuelconsumptionColor1 = "orange";
        this.fuelconsumptionColor2 = "#849fca";
        this.fuelconsumptionColor3 = "#849fca";
        this.fuelconsumptionColor4 = "#849fca";
        this.fuelconsumptionColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.fuelconsumptionColor1 = "#849fca";
        this.fuelconsumptionColor2 = "orange";
        this.fuelconsumptionColor3 = "#849fca";
        this.fuelconsumptionColor4 = "#849fca";
        this.fuelconsumptionColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.fuelconsumptionColor1 = "#849fca";
        this.fuelconsumptionColor2 = "#849fca";
        this.fuelconsumptionColor3 = "orange";
        this.fuelconsumptionColor4 = "#849fca";
        this.fuelconsumptionColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.fuelconsumptionColor1 = "#849fca";
        this.fuelconsumptionColor2 = "#849fca";
        this.fuelconsumptionColor3 = "#849fca";
        this.fuelconsumptionColor4 = "orange";
        this.fuelconsumptionColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.fuelconsumptionColor1 = "#849fca";
        this.fuelconsumptionColor2 = "#849fca";
        this.fuelconsumptionColor3 = "#849fca";
        this.fuelconsumptionColor4 = "#849fca";
        this.fuelconsumptionColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.comfort,
        this.brand2Datas.comfort,
        this.brand3Datas.comfort,
        this.brand4Datas.comfort,
        this.brand5Datas.comfort
      );
      if (brand == "brand1") {
        this.comfortColor1 = "orange";
        this.comfortColor2 = "#849fca";
        this.comfortColor3 = "#849fca";
        this.comfortColor4 = "#849fca";
        this.comfortColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.comfortColor1 = "#849fca";
        this.comfortColor2 = "orange";
        this.comfortColor3 = "#849fca";
        this.comfortColor4 = "#849fca";
        this.comfortColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.comfortColor1 = "#849fca";
        this.comfortColor2 = "#849fca";
        this.comfortColor3 = "orange";
        this.comfortColor4 = "#849fca";
        this.comfortColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.comfortColor1 = "#849fca";
        this.comfortColor2 = "#849fca";
        this.comfortColor3 = "#849fca";
        this.comfortColor4 = "orange";
        this.comfortColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.comfortColor1 = "#849fca";
        this.comfortColor2 = "#849fca";
        this.comfortColor3 = "#849fca";
        this.comfortColor4 = "#849fca";
        this.comfortColor5 = "orange";
      }
      brand = this.findMax(
        this.brand1Datas.optionsandfeatures,
        this.brand2Datas.optionsandfeatures,
        this.brand3Datas.optionsandfeatures,
        this.brand4Datas.optionsandfeatures,
        this.brand5Datas.optionsandfeatures
      );
      if (brand == "brand1") {
        this.optionsandfeaturesColor1 = "orange";
        this.optionsandfeaturesColor2 = "#849fca";
        this.optionsandfeaturesColor3 = "#849fca";
        this.optionsandfeaturesColor4 = "#849fca";
        this.optionsandfeaturesColor5 = "#849fca";
      } else if (brand == "brand2") {
        this.optionsandfeaturesColor1 = "#849fca";
        this.optionsandfeaturesColor2 = "orange";
        this.optionsandfeaturesColor3 = "#849fca";
        this.optionsandfeaturesColor4 = "#849fca";
        this.optionsandfeaturesColor5 = "#849fca";
      } else if (brand == "brand3") {
        this.optionsandfeaturesColor1 = "#849fca";
        this.optionsandfeaturesColor2 = "#849fca";
        this.optionsandfeaturesColor3 = "orange";
        this.optionsandfeaturesColor4 = "#849fca";
        this.optionsandfeaturesColor5 = "#849fca";
      } else if (brand == "brand4") {
        this.optionsandfeaturesColor1 = "#849fca";
        this.optionsandfeaturesColor2 = "#849fca";
        this.optionsandfeaturesColor3 = "#849fca";
        this.optionsandfeaturesColor4 = "orange";
        this.optionsandfeaturesColor5 = "#849fca";
      } else if (brand == "brand5") {
        this.optionsandfeaturesColor1 = "#849fca";
        this.optionsandfeaturesColor2 = "#849fca";
        this.optionsandfeaturesColor3 = "#849fca";
        this.optionsandfeaturesColor4 = "#849fca";
        this.optionsandfeaturesColor5 = "orange";
      }
    },

    getBrand1Datas() {
      if (this.select2 != "") {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select2,
            date: this.value,
          },
        }).then((resp) => {
          this.brand1Datas = resp.data;
          this.showBrand1Datas();
          this.list1style = "border-left: 1px solid rgb(2,40,120)";
          this.brand1Num = resp.data.datanum;
          this.select1Brand = resp.data.brand;

          this.getpiedata(this.select1Brand, this.pieOption, 0);
        });
      } else {
        this.list1style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand2Datas() {
      if (this.select3.length >= 1) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[0],
            date: this.value,
          },
        }).then((resp) => {
          this.brand2Datas = resp.data;
          this.showBrand1Datas();
          this.list2style = "border-left: 1px solid rgb(2,40,120)";
          this.brand2Num = resp.data.datanum;
          this.select2Brand = resp.data.brand;

          this.getpiedata(this.select2Brand, this.pieOption1, 1);
        });
      } else {
        this.list2style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand3Datas() {
      if (this.select3.length >= 2) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[1],
            date: this.value,
          },
        }).then((resp) => {
          this.brand3Datas = resp.data;
          this.showBrand1Datas();
          this.list3style = "border-left: 1px solid rgb(2,40,120)";
          this.brand3Num = resp.data.datanum;
          this.select3Brand = resp.data.brand;

          this.getpiedata(this.select3Brand, this.pieOption2, 2);
        });
      } else {
        this.list3style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand4Datas() {
      if (this.select3.length >= 3) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[2],
            date: this.value,
          },
        }).then((resp) => {
          this.brand4Datas = resp.data;
          this.showBrand1Datas();
          this.list4style = "border-left: 1px solid rgb(2,40,120)";
          this.brand4Num = resp.data.datanum;
          this.select4Brand = resp.data.brand;
        });
      } else {
        this.list4style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    getBrand5Datas() {
      if (this.select3.length >= 4) {
        this.axios({
          url: "/api/koubei/selectAllByName",
          method: "POST",
          params: {
            name: this.select3[3],
            date: this.value,
          },
        }).then((resp) => {
          this.brand5Datas = resp.data;
          this.showBrand1Datas();
          this.list5style = "border-left: 1px solid rgb(2,40,120)";
          this.brand5Num = resp.data.datanum;
          this.select5Brand = resp.data.brand;
        });
      } else {
        this.list5style = "border-left: 0px solid rgb(2,40,120)";
      }
    },
    selectChange() {
      this.getkoubeNum();
      this.brand1Datas = {
        exterior: "",
        interior: "",
        comfort: "",
        carspace: "",
        power: "",
        fuelconsumption: "",
        optionsortrim: "",
        maneuverability: "",
      };
      this.brand2Datas = {
        exterior: "",
        interior: "",
        comfort: "",
        carspace: "",
        power: "",
        fuelconsumption: "",
        optionsortrim: "",
        maneuverability: "",
      };
      this.brand3Datas = {
        exterior: "",
        interior: "",
        comfort: "",
        carspace: "",
        power: "",
        fuelconsumption: "",
        optionsortrim: "",
        maneuverability: "",
      };
      this.brand4Datas = {
        exterior: "",
        interior: "",
        comfort: "",
        carspace: "",
        power: "",
        fuelconsumption: "",
        optionsortrim: "",
        maneuverability: "",
      };
      this.brand5Datas = {
        exterior: "",
        interior: "",
        comfort: "",
        carspace: "",
        power: "",
        fuelconsumption: "",
        optionsortrim: "",
        maneuverability: "",
      };
      this.list1style = "border-left: 0px solid rgb(2,40,120)";
      this.list2style = "border-left: 0px solid rgb(2,40,120)";
      this.list3style = "border-left: 0px solid rgb(2,40,120)";
      this.list4style = "border-left: 0px solid rgb(2,40,120)";
      this.list5style = "border-left: 0px solid rgb(2,40,120)";

      this.getBrand1Datas();
      this.getBrand2Datas();
      this.getBrand3Datas();
      this.getBrand4Datas();
      this.getBrand5Datas();
    },
    getpieOption() {},
    getpieOption1() {},
    getpieOption2() {},
    btn1() {
      this.show1 = true;
      this.show2 = false;
      this.koubeiHeaders = true;
      this.headers = false;
    },
    btn2() {
      this.show1 = false;
      this.show2 = true;
      this.koubeiHeaders = false;
      this.headers = true;
    },
    handleResize() {
      this.pieCharts.resize();

      this.pieCharts1.resize();
      this.pieCharts2.resize();
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
  width: 530px;
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
  left: 352px;
  font-size: 18px;
}
.brand3 {
  position: absolute;
  top: 45px;
  left: 570px;
  font-size: 18px;
}
.brand4 {
  position: absolute;
  top: 45px;
  left: 770px;
  font-size: 18px;
}
.brand5 {
  position: absolute;
  top: 45px;
  left: 970px;
  font-size: 18px;
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
  left: 632px;
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
/deep/.el-progress-bar__outer {
  // height: 1.4vw !important;
}
</style>