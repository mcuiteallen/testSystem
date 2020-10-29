<template>
  <div class="mainLayout" > 
    <div class="mainContent">      
        <div class="row justify-content-center" >
          <button type="button" class="btn btn-primary priceBtn" style="margin-top: 50px;font-weight: bold;" @click="openTest1Modal('start')" > 正式測驗 </button>                
        </div>
        <div class="row justify-content-center" >
          <button type="button" class="btn btn-primary priceBtn" style="margin-top: 50px;font-weight: bold;" @click="openTest1Modal('keep')" > 重複測驗 </button>                
        </div>        
    </div>
    <div class="fixed-bottom footer row justify-content-center" style="background-color: rgba(51, 51, 51, 0.75);">
      <footer class="footerCss">
        AllenKao&nbsp;版權所有@2020</footer>
    </div>
    <vuestic-modal
      v-bind:force="true"
      v-bind:large="true"
      ref="test1"
      @cancel="cancelTest1Modal()"
    >  
      <loading :active.sync="isLoading" :can-cancel="false" :is-full-page="fullPage"></loading>
      <div slot="title">{{testName}} {{allTest1Count}}/{{current1Count}}</div>  
      <div v-if="unselectTopic">
        <div class="row justify-content-center" >
          <button type="button" class="btn btn-primary priceBtn" style="margin-top: 50px;font-weight: bold;" @click="openTest1Modal('start')" > 正式測驗 </button>                
        </div>
        <div class="row justify-content-center" >
          <button type="button" class="btn btn-primary priceBtn" style="margin-top: 50px;font-weight: bold;" @click="openTest1Modal('keep')" > 重複測驗 </button>                
        </div>           
      </div>      
      <div v-else>
        <div v-show="current1Count <= allTest1Count" class="row justify-content-end" style="width: 100%;margin-left: 0px;margin-right: 0px;">   
          <button
            type="button"
            class="btn-primary justify-content-center"
            v-on:click="ans()"
            style="border-radius: 15px;outline: none;"
          >ans</button>        
          <button
            type="button"
            class="btn-primary justify-content-center"
            v-on:click="next()"
            style="margin-left: 10px;border-radius: 15px;outline: none;"
          >next</button>            
        </div> 
        <div v-show="current1Count <= allTest1Count" class="row justify-content-center" style="width: 100%;margin-left: 0px;margin-right: 0px;">       
          <img style="width: 100%;margin-top: 10px" :src="current1Test">
        </div>    
        <div v-show="showAns && current1Count <= allTest1Count" class="row justify-content-start" style="width: 100%;margin-left: 0px;margin-right: 0px;">       
          <img style="width: 100%;margin-top: 50px" :src="current1Ans">
          <button
            v-show="current1Count <= allTest1Count"
            type="button"
            class="btn-primary"
            v-on:click="keep()"
            style="margin-left: 10px;border-radius: 15px;outline: none;"
          >keep</button>     
          {{current1Ans}}   
        </div>     
        <div v-show="current1Count > allTest1Count" class="row justify-content-center" style="width: 100%;margin-left: 0px;margin-right: 0px;">       
          <h2>Test Finish</h2>
        </div>          
      </div>
           
      <div slot="footer">
        <button
          v-show="current1Count > allTest1Count"
          type="button"
          class="btn btn-primary"
          v-on:click="next()"
        >Test End</button>        
      </div>    
    </vuestic-modal>     
  </div>
</template>

<script>
import Vue from "vue";
import VueLoading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";
import Apis from '@/util/Apis'

let self = {};
export default {
  name: "v-main",
  components: {
    loading: VueLoading    
  },
  data() {
    return {
      isLoading: false,
      fullPage: false,      
      testName: '',
      keepTest: [],
      test1: [],
      opened: true,
      allTest1Count: '',
      current1Test: '',  
      current1Ans: '',    
      current1Count: 1,
      showAns: false,
      countInput: '',
      unselectTopic: '',
    };
  },
  created () {
  },
  mounted() {
    self = this  
  },  
  methods: {
    async init(type) {
      self.test1 = []
      self.current1Count = 1
      if(type === 'keep'){
        self.testName = '再次測驗'
        self.test1 = self.keepTest
        self.allTest1Count = self.keepTest.length
      }else{
        self.testName = '正式測驗'
        self.allTest1Count = 10000
        
        self.isLoading = true
        for(let i = 1 ; i <= self.allTest1Count ; i++){
          let fso = '/static/img/test1/' + i + '.jpg'
          let res = await Apis.file.get.jsonFile(fso)
          .catch(function (error) {
            
          })
          if(res){  
            self.test1.push(fso)  
          }else{
            self.allTest1Count = i - 1
            self.isLoading = false
            break
          }                         
        }    
          
        self.test1.sort(function() {
            return (0.5-Math.random());
        });  
      }      
      self.current1Test = self.test1[self.current1Count-1]
    },
    openTest1Modal (type) {
      if(self.unselectTopic){

      }else{
        self.init(type)
      }
      self.$refs.test1.open()
    },        
    cancelTest1Modal () {
      self.$refs.test1.close()
    }, 
    keep() {
      let repeat = false
      for(let i = 0 ; i < self.keepTest.length ; i++){
        if(self.keepTest[i] === self.current1Test){
          repeat = true
          break
        }
      }
      if(!repeat){
        self.keepTest.push(self.current1Test)
      }
    },
    next(){
      self.showAns = false
      if(self.current1Count > self.allTest1Count){
        self.test1 = []      
        self.current1Count = 1
        self.current1Test = self.test1[self.current1Count-1]
        self.cancelTest1Modal()
      }else{
        self.current1Count = self.current1Count + 1
        self.current1Test = self.test1[self.current1Count-1]
      }    
    },
    ans(){
      self.showAns = true
      self.current1Ans = self.current1Test.replace('.jpg', '_ans.jpg')
    },   
  },
  beforeDestroy() {}
};
</script>

<style scoped lang="scss">
.mainLayout {
  padding: 0rem;
  background-color: #ffffff
}
.mainContent {
  width: 100uw;

  //height: 100uh;
  background: #333333;
}
.priceBtn{
  background-color: #fbfbfb;  
  color: #333333; 
}  
.header-img {
  width: 30%;
  height: 100%;
  background-size: cover;
  overflow: hidden;
}
.navbar-dark .navbar-nav .nav-link {
    color: #ffffff;
    font-family:微軟正黑體;
    font-size: 180%
}
.navImg {
  font-size: 100%; 
  @media (max-width:483px) {
    font-size: 0%;
    margin-left: 100%;  

  }  
}
.navbar .navbar-nav .nav-item .nav-link {
  padding-right: 15px;
  padding-left: 15px;
  line-height: 0;
}
.label {
    display: inline-block;
    margin-bottom: 0rem;
    font-size: 172%;
    @media (max-width:483px) {
      font-size: 0%; 
    }      
}
.labelPhone {
    display: inline-block;
    margin-bottom: 0rem;
    font-size: 0%;
    @media (max-width:483px) {
      font-size: 80%; 
    }      
}
.footerCss {
  font-size: 16px;
  color:#FFFFFF; 
}
</style>
