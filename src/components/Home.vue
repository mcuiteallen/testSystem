<template>
  <div>
      <vuestic-widget class="no-v-padding homeNavCss " >
        <loading :active.sync="isLoading" :can-cancel="false" :is-full-page="fullPage"></loading>
        <div class="row justify-content-center backgroundDiv">
          <img class="sopImg" src="/static/img/home/background.jpg">    
        </div>    
        <div class="row justify-content-center logoDiv">
          <img class="logoImg" src="/static/img/home/logo.png">     
        </div>          
        <div class="row justify-content-center" >
          <h3 class="header3" >為您的愛車找到下一個愛他的主人</h3>
          <!--<h3 class="header3" >線上估車-行情加3萬跟您收購</h3>-->
          <!--<p>联系电话：<a :href="'tel:0987831160'">0987831160</a></p>-->
        </div>             
        <div class="row justify-content-center imgDiv" >
          <img  class="buttonImg priceImg" src="/static/img/home/price.png" >  
          <img  class="buttonImg transactionImg" src="/static/img/home/transaction.png">
          <!--<div class="col-md-3">
            <img @click="openModal()" class="buttonImg" src="/static/img/home/bossLine.png" >
            <img @click="openModal()" class="buttonImg" style="" src="/static/img/home/addfriends_en.png" >
          </div> -->                    
        </div>          
        <div class="row justify-content-center buttonImgDiv" >
          <button type="button" class="btn btn-primary priceBtn"  @click="openModal()" > 為您估價 </button>
          <button type="button" class="btn btn-primary transactionBtn"  @click="chooseMenu(2)" > 交易流程 </button>
          <button type="button" class="btn btn-primary sampleBtn"  @click="chooseMenu(3)" > 成交案例 </button>
          <!--<div class="col-md-3">
            <img @click="openModal()" class="buttonImg" src="/static/img/home/bossLine.png" >
            <img @click="openModal()" class="buttonImg" style="" src="/static/img/home/addfriends_en.png" >
          </div> -->                    
        </div> 
        <div class="row justify-content-center phoneDiv" >
          <p ><a @click="openWindows()"><img class="lineButtonByPhone" src="/static/img/home/LINEIMG.png"> </a>  </p>
          <p ><a :href="'tel:0926624664'"><img class="phoneButtonByPhone" src="/static/img/home/PHONEIMG.png "></a> </p>                         
        </div>
        <!--<div class="row justify-content-start" >
          <img @click="openModal()" class="lineImg" src="/static/img/home/bossLine.png" >                  
        </div>-->   
        <div class="row justify-content-start" >
          <img @click="openLineModal()" class="lineButtonImg" src="/static/img/home/LINEIMG.png">                  
        </div>   
        <!--<div class="row justify-content-start" >
          <img @click="openLineModal()" class="phoneButtonImg" src="/static/img/home/PHONEIMG.png">                  
        </div>-->         
        <!--<div class="row justify-content-start" >
          <img @click="openLineModal()" class="lineButtonImg" src="/static/img/home/LINEIMG.png">               
        </div>-->                            
        <!--<img @click="chooseMenu(2)" class="fiexd-QRCode" src="/static/img/home/bossLine.png">          
        <img @click="chooseMenu(2)" class="fiexd-Add-friend" src="/static/img/home/addfriends_en.png">-->
        <!--<div class="row justify-content-center">
          <button type="button" class="btn btn-primary"  @click="openModal()" > 馬上估車 </button>
        </div>-->  
    <vuestic-modal
      v-bind:force="true"
      v-bind:large="true"
      ref="ModalSaleInfo"
      @cancel="cancelModal()"
    >
      <loading :active.sync="isLoading" :can-cancel="false" :is-full-page="fullPage"></loading>
      <div slot="title">估車資訊</div>
      <div>
        <div class="row">
          <div class="col-md-12">
            <fieldset>
              <div
                class="form-group with-icon-right"
              >
                <div class="input-group">
                  <input name="nameInput" v-model="nameInput" v-validate="'required'" />
                  <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                  <i class="fa fa-check valid-icon icon-right input-icon"></i>
                  <label
                    class="control-label"
                    for="nameInput"
                  >您的大名</label>
                  <i class="bar"></i>
                </div>
              </div>
            </fieldset>
          </div>  
        </div>          
        <div class="row">
          <div class="col-md-6">
            <!--<vuestic-simple-select
              label="廠牌"
              v-model="selectFactory"
              option-key="name"
              v-bind:options="factoryList"
              :unselect-disabled="false"
              :notCollapse="true"
              :showSearchBox="false"
              :searchText="$t('deviceon.device.view.searchText')"
            />-->
            <fieldset>
              <div
                class="form-group with-icon-right"
              >
                <div class="input-group">
                  <input name="factoryInput" v-model="factoryInput" v-validate="'required'" />
                  <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                  <i class="fa fa-check valid-icon icon-right input-icon"></i>
                  <label
                    class="control-label"
                    for="factoryInput"
                  >廠牌 & 車款</label>
                  <i class="bar"></i>
                </div>
              </div>
            </fieldset>            
          </div> 
          <div class="col-md-6">
            <fieldset>
              <div
                class="form-group with-icon-right"
              >
                <div class="input-group">
                  <input name="yearInput" v-model="yearInput"  type="number"  v-validate="'required'" />
                  <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                  <i class="fa fa-check valid-icon icon-right input-icon"></i>
                  <label
                    class="control-label"
                    for="yearInput"
                  >年份</label>
                  <i class="bar"></i>
                </div>
              </div>
            </fieldset>             
          </div>           
        </div>     
        <div class="search-box">
          <div class="row">
            <div class="col-md-6">
              <vuestic-simple-select
                label="車子所在地"
                v-model="selectLocate"
                option-key="name"
                v-bind:options="locateList"
                :unselect-disabled="true"
                :notCollapse="true"
                :showSearchBox="false"
                searchText="搜尋"
              />
            </div> 
            <div class="col-md-6">
              <fieldset>
                <div
                  class="form-group with-icon-right"
                >
                  <div class="input-group">
                    <input name="milageInput" v-model="milageInput" type="number" v-validate="'required'" />
                    <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                    <i class="fa fa-check valid-icon icon-right input-icon"></i>
                    <label
                      class="control-label"
                      for="milageInput"
                    >里程數</label>
                    <i class="bar"></i>
                  </div>
                </div>
              </fieldset>
            </div>           
          </div> 
          <div class="row">
            <div class="col-md-6">
              <fieldset>
                <div
                  class="form-group with-icon-right"
                >
                  <div class="input-group">
                    <input name="lineIdInput" v-model="lineIdInput" v-validate="'required'" />
                    <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                    <i class="fa fa-check valid-icon icon-right input-icon"></i>
                    <label
                      class="control-label"
                      for="lineIdInput"
                    >Line ID</label>
                    <i class="bar"></i>
                  </div>
                </div>
              </fieldset>            
            </div> 
            <div class="col-md-6">
              <fieldset>
                <div
                  class="form-group with-icon-right"
                >
                  <div class="input-group">
                    <input name="phoneInput" v-model="phoneInput" type="number" v-validate="'required'" />
                    <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                    <i class="fa fa-check valid-icon icon-right input-icon"></i>
                    <label
                      class="control-label"
                      for="phoneInput"
                    >電話</label>
                    <i class="bar"></i>
                  </div>
                </div>
              </fieldset>   
            </div>           
          </div> 
        </div>        
        <div class="row">
          <div class="col-md-12">
            <fieldset>
              <div
                class="form-group with-icon-right"
              >
                <div class="input-group">
                  <input name="prePriceInput" v-model="prePriceInput" type="number" v-validate="'required'" />
                  <i class="fa fa-exclamation-triangle error-icon icon-right input-icon"></i>
                  <i class="fa fa-check valid-icon icon-right input-icon"></i>
                  <label
                    class="control-label"
                    for="prePriceInput"
                  >期待售出金額</label>
                  <i class="bar"></i>
                </div>
              </div>
            </fieldset>   
          </div>           
        </div>                       
        <!--
            <div class="form-group with-icon-right" :class="{'has-error': errors.has('txtSMSPhone')}">
              <div class="input-group">
                <vue-phone-number-input
                  v-model="Phone"
                  ref="phone"
                  name="txtSMSPhone"
                  data-vv-as="Recipient Phone"
                  v-validate="'required'"
                  color="red"
                  @update="onPhone"
                  :translations="phoneTranslations"
                  :error="hasPhoneErrorActive"
                  size="lg"
                />
              </div>
            </div>            
        -->
                        
        <vuestic-file-upload
          type="gallery"
          :btnName = btnName
          v-model="imgFiles"
          fileTypes=".png,.jpg,.jpeg,.gif"
        />
      </div>
      <div slot="footer">
        <button
          type="button"
          class="btn btn-primary"
          v-on:click="sendToBoss()"
        >送出</button>
      </div>
    </vuestic-modal>   
    <vuestic-modal
      v-bind:force="true"
      v-bind:large="true"
      ref="AddLine"
      :noButtons="true"
    >
      <div class="row justify-content-center">
        <img @click="openWindows()"  class="addLine" src="/static/img/home/bossLine.png">          
      </div>
      <div class="row justify-content-center">       
        <img @click="openWindows()" class="addLine" style="margin-top: 10px" src="/static/img/home/addfriends_en.png">
      </div>    
    </vuestic-modal>                                     
      </vuestic-widget>
  </div>
</template>

<script>
import Vue from 'vue'
import VueLoading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";
import Apis from '@/util/Apis'

let self = {};
export default {
  name: "Home",
  computed: {},
  components: {
    loading: VueLoading
  },
  data() {
    return {
      isLoading: false,
      fullPage: false,
      imgFiles: [],
      btnName: '上傳照片',
      newImgSrc: '',
      defaultLogo: '',
      isHasMessageBox: true,    
      //selectFactory: '',
      //factoryList: [{name: '寶馬'},{name: '賓士'}],
      yearInput: '',
      //yearList: [{name: '1990以下'},{name: '1991~1995'},{name: '1996~2000'},{name: '2001~2005'},{name: '2006~2010'},{name: '2011~2015'},{name: '2016~2020'}],      
      milageInput: '',
      prePriceInput: '',
      //milageList: [{name: '3萬以下'},{name: '5萬以下'},{name: '10萬以下'},{name: '15萬以下'},{name: '20萬以下'},{name: '30萬以下'},{name: '50萬以下'}],  
      selectLocate: '',
      locateList: [{name: '台北市'},{name: '新北市'},{name: '基隆市'},{name: '宜蘭縣/市'},{name: '桃園市'},{name: '新竹縣/市'},{name: '苗栗縣/市'},{name: '台中市'},{name: '彰化縣/市'},{name: '雲林縣'},{name: '嘉義縣/市'},{name: '台南縣/市'},{name: '高雄縣/市'},{name: '屏東縣/市'},{name: '台東縣/市'},{name: '花蓮縣/市'}],    
      //locateList: [{name: '北北基'},{name: '桃竹苗'},{name: '中彰雲'},{name: '宜蘭'},{name: '花東'},{name: '高屏'}],    
      nameInput: '',   
      factoryInput: '', 
      Phone: '',
      PhoneFormat: false,
      onChangePhone: true,
      showPhone: true,     
      phoneInput: '',  
      lineIdInput: '',  
      hasPhoneErrorActive: false,    
      inputIsValid: false,    
      //phoneTranslations: {
      //  countrySelectorLabel: '',
      //  countrySelectorError: '',
      //  phoneNumberLabel: '',
      //  example: 'Exemple :'
      //},           
    };
  },
  mounted() {
    self = this
  },  
  watch: {},
  computed:{
  },  
  methods: {       
    openModal () {
      self.$refs.ModalSaleInfo.open()
    },
    openLineModal () {
      self.$refs.AddLine.open()
    }, 
    openWindows() {
      window.open('https://line.me/ti/p/trvCNPQC5u', '_blank')
    },   
    chooseMenu (tabId) {
      this.$bus.$emit('menuChange', {id: tabId})      
    },   
    cancelModal () {
      self.clearInput()
      self.$refs.ModalSaleInfo.close()
      self.$refs.AddLine.close()
    },  
    clearInput () {
      //self.selectFactory = ''
      self.yearInput = ''
      self.milageInput = ''
      self.prePriceInput = ''
      self.selectLocate = ''
      //self.PhoneFormat = false
      //self.Phone = ''
      self.lineIdInput = ''
      self.phoneInput = ''
      self.nameInput = ''
      self.factoryInput = ''
      self.imgFiles = []
      setTimeout(function () {
        self.errors.clear()
      }, 10)         
    }, 
    //onPhone (Data) {
    //  if (this.Phone !== '') {
    //    this.onChangePhone = false
    //  }
    //  this.PhoneFormat = false
    //  if (Data.isValid) {
    ////    this.PhoneFormat = true
    //  }
    //  this.PhoneInput = Data
    //},  
    buttonEnable () {
      if (self.selectLocate !== '') {
        if (self.nameInput.trim() !== '' && self.yearInput.trim() !== ''  && self.milageInput.trim() !== ''  && self.prePriceInput.trim() !== ''  && self.factoryInput.trim() !== '' && self.phoneInput.trim() !== '' && self.lineIdInput.trim() !== '') {
          return true
        } else return false
      } else {
        return false
      }
    }, 
    dataURItoBlob(dataURI) {
        var byteString = atob(dataURI.split(',')[1]);
        var mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];
        var ab = new ArrayBuffer(byteString.length);
        var ia = new Uint8Array(ab);
        for (var i = 0; i < byteString.length; i++) {
            ia[i] = byteString.charCodeAt(i);
        }
        return new Blob([ab], {type: mimeString});
    },         
    sendToBoss () {
      let manyImg = self.imgFiles    
      let pictureNameList = []    
      if(self.buttonEnable()){
        if(manyImg.length > 0){
          if (manyImg.length >= 5) {
            Apis.MessageBox.Normal(
              self,
              '照片已超過上傳數量!!',
              '',
              'warning'
            )
            return false
          }
          for(let j = 0 ; j < manyImg.length ; j++){
            let tmpData = manyImg[j]
            let orgName = tmpData.name.split('.')
            let pictureNum = j+1
            pictureNameList.push('picture' + pictureNum + '.' + orgName[1])
          }
          self.isLoading = true
          let session = self.nameInput + Date.now()
          let carDetail = {}
          carDetail['Name'] = self.nameInput
          carDetail['Phone'] = self.phoneInput
          carDetail['LineID'] = self.lineIdInput
          //carDetail['Factory'] = self.selectFactory.name
          carDetail['Factory'] = self.factoryInput
          carDetail['Year'] = self.yearInput
          carDetail['Milage'] = self.milageInput
          carDetail['PrePrice'] = self.prePriceInput
          carDetail['Locate'] = self.selectLocate.name
          carDetail['pictureNameList'] = pictureNameList
          let message = '\n大名: ' + carDetail.Name + '\n' + 
            '電話: ' + carDetail.Phone + '\n' + 
            'LINE ID: ' + carDetail.LineID + '\n' + 
            '廠牌: ' + carDetail.Factory + '\n' +
            '年份: ' + carDetail.Year + '\n' + 
            '里程: ' + carDetail.Milage + '\n' +
            '所在地: ' + carDetail.Locate + '\n' +
            '期望售出金額: ' + carDetail.PrePrice + '\n'  
          for(let i = 0 ; i < manyImg.length ; i++){
            let fd = new FormData();
            let tmpFile = manyImg[i]
            let pictureNum = i+1
            let lastest = false
            if(i === manyImg.length-1){
              lastest = true
            }
            let reader = new FileReader()
            reader.readAsDataURL(tmpFile)
            reader.onload = function (e) {
              let Img = new Image()
              let canvas = document.createElement('canvas')
              let context = canvas.getContext('2d')
              canvas.width = 1000
              canvas.height = 800
              Img.src = this.result
              context.drawImage(Img, 0, 0, canvas.width, canvas.height);
              if (tmpFile.type === 'image/jpeg' || tmpFile.type === 'image/jpg') {
                Img.src = canvas.toDataURL('image/jpeg', 0.8)
              } else if (tmpFile.type === 'image/gif') {
              } else {
                Img.src = canvas.toDataURL()
              }              
              let blob = self.dataURItoBlob(Img.src);
              fd.append('myImage', blob, tmpFile.name)
              fd.append('session', session) 
              fd.append('newName', 'picture' + pictureNum.toString())   
              fd.append('message', message) 
              fd.append('orgName', tmpFile.name) 
              fd.append('pictureNameList', carDetail['pictureNameList'].toString())
              fd.append('lastData', lastest) 
              let api = '/uploadPhoto'

              Apis.uploadImg.post
                .uploadByFormData(fd)
                .then(function (xhr) {
                  if(lastest){
                    self.isLoading = false
                    //self.cancelModal()
                    Apis.MessageBox.Normal(
                      self,
                      '送出成功!!',
                      '經過評估過後會立即連絡您，請耐心等候~',
                      'success'
                    ).then(
                      self.cancelModal()
                    )
                  }
                })
                .catch(function (error) {
                  self.isLoading = false
                })    
            }           
          }
        }               
      }else{
        Apis.MessageBox.Normal(
          self,
          '有資料沒填到喔',
          '或是格式不正確喔',
          'warning'
        )
      }
    },          
  },
  beforeDestroy() {
    self.cancelModal
  }
};
</script>

<style scoped lang="scss">
.content {
  padding: 1rem;
  margin-top: 8%;
  min-height: auto;
  background-color: #ffffff;
  @media (max-width:1024px){
    margin-top: 12%; 
  }
  @media (max-width:768px){
    margin-top: 15%;
  }     
  @media (max-width:483px) {
    margin-top: 36%;    
  }    
} 
.btn{
  margin: 20px 0;
  width: 262px;
  height: 58px;
  line-height: 0px;
  min-height: auto;
  //border: 1px solid #ccc;
  font-size: 30px;
  font-weight: 900;
  text-align: center;  
  @media (max-width:483px) {
    font-size: 23px;
    height: 48px;
    width: 230px;
    padding: 10px;
  }  
  @media (max-width:375px) {
    font-size: 23px;
    height: 48px;
    width: 203px;
    padding: 10px;
  }    
  @media (max-width:320px) {
    font-size: 23px;
    height: 48px;
    width: 177px;
    padding: 10px;
  }     
}
.btn:hover {
    background-color: #bebebe; 
}
.sopImg{
  min-height: auto;
  width: 100%;  
  filter: brightness(38%);
  @media screen and (max-height: 1400px) and (max-width: 1024px){  
    filter: brightness(100%);
  }    
  @media screen and (max-height: 823px) and (max-width: 483px){  
    width: 0%; 
  }  
}
.logoImg{
  min-height: auto;
  width: 0%;  
  @media screen and (max-height: 823px) and (max-width: 483px){  
    width: 50%; 
  }   
}
.buttonImg{
  padding-top: 5%;
  width: 10%;  
  min-height: auto;
  @media (max-width:1024px){
    padding-top: 0%;
    width: 15%;
  }
  @media (max-width:768px){
    padding-top: 0%;
    width: 20%;
  }     
  @media (max-width:483px) {
    padding-top: 0%;
    width: 25%;
  }   
  @media (max-width:320px) {
    padding-top: 0%;
    width: 25%;
  }    
}
.buttonImgDiv{
  @media screen and (max-height: 823px) and (max-width: 375px){     
    margin-top: 0%;
  }  
  @media screen and (max-height: 823px) and (max-width: 320px){     
    margin-top: 10%;
  }    
}
.phoneDiv{
  margin-top: -3%;
  @media screen and (max-height: 823px) and (max-width: 375px){     
    margin-top: 0%;
  }    
}
.transactionImg{
  position: fixed;
  margin-left: 15%;
  margin-top: -67%; 
  min-height: auto;
  @media (max-width:1024px){
    margin-left: 15%;
    margin-top: 18%; 
    position: unset;
  }
  @media (max-width:768px){
    margin-left: 23%;
    position: unset;
  }     
  @media (max-width:483px) {
    margin-left: 10%;
    position: unset;
    width: 0%;
  }   
  @media (max-width:320px) {
    margin-left: 5%;
    position: unset;
  }    
}
.transactionBtn{
  position: fixed;
  margin-left: 15%;
  margin-top: -51%; 
  //background-color: #333333;
  min-height: auto;
  background-color: #fbfbfb;    
  color: #333333;  
  @media (max-width:1024px){
    margin-left: 5%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;    
  }
  @media (max-width:768px){
    margin-left: 10%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }     
  @media (max-width:483px) {
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }   
  @media (max-width:320px) {
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }    
}
.priceImg{
  position: fixed;
  margin-left: -15%;
  margin-top: -67%; 
  min-height: auto;
  @media (max-width:1024px){
    margin-left: 0%;
    margin-top: 18%; 
    position: unset;
  }
  @media (max-width:768px){
    margin-left: 0%;
    position: unset;
  }     
  @media (max-width:483px) {
    margin-left: 0%;
    position: unset;
    width: 0%;
  }   
  @media (max-width:320px) {
    margin-left: 0%;
    position: unset;
  }    
}
.priceBtn{
  position: fixed;
  margin-left: -15%;
  margin-top: -51%; 
  min-height: auto;
  background-color: #fbfbfb;  
  color: #333333; 
  @media (max-width:1024px){
    margin-left: 0%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }
  @media (max-width:768px){
    margin-left: 0%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }     
  @media (max-width:483px) {
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }   
  @media (max-width:320px) {
    margin-top: -14%;
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }    
}
.sampleBtn{
  position: fixed;
  margin-left: 1000%;
  margin-top: -51%; 
  min-height: auto;
  background-color: #fbfbfb;  
  color: #333333; 
  @media (max-width:1024px){
    margin-left: 1000%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }
  @media (max-width:768px){
    margin-left: 1000%;
    margin-top: 3%; 
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }     
  @media (max-width:483px) {
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }   
  @media (max-width:320px) {
    margin-top: 2%;
    margin-left: 0%;
    position: unset;
    background-color: #333333;    
    color: #ffffff;      
  }    
}
.backgroundDiv{
  //height: 600px;
  min-height: auto;
  @media screen and (max-height: 823px) and (max-width: 1024px){  
    position: unset;
    min-height: auto;
    height: auto;
  }
  @media screen and (max-height: 823px) and (max-width: 768px){    
    position: unset;
    min-height: auto;
    height: auto;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){  
    position: unset;
    min-height: auto;
    max-height:275px;
  }   
  @media screen and (max-height: 823px) and (max-width: 375px){  
    position: unset;
    min-height: auto;
    max-height:275px;
  } 
  @media screen and (max-height: 823px) and (max-width: 320px){
    max-height:275px;
  }   
}
.logoDiv{
  //height: 600px;
  min-height: auto;
  @media screen and (max-height: 823px) and (max-width: 1024px){  
    position: unset;
    min-height: auto;
    height: auto;
  }
  @media screen and (max-height: 823px) and (max-width: 768px){    
    position: unset;
    min-height: auto;
    height: auto;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){  
    position: unset;
    min-height: auto;
    max-height:275px;
  }   
}
.imgDiv{ 
  @media screen and (max-height: 823px) and (max-width: 483px){     
    max-height: 10px;
  }  
  @media screen and (max-height: 823px) and (max-width: 414px){     
    max-height: 50px;
  } 
  @media screen and (max-height: 823px) and (max-width: 320px){     
    max-height: 44px;
  }       
}
.lineButtonByPhone{
  width: 0%;
  @media screen and (max-height: 1366px) and (max-width: 1024px){  
    width: 0%;
  }
  @media screen and (max-height: 1024px) and (max-width: 768px){     
    width: 0%;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){     
    width: auto;
    max-height: 65px;
  }      
}
.phoneButtonByPhone{
  width: 0%;
  margin-left: 5%;
  @media screen and (max-height: 1366px) and (max-width: 1024px){  
    width: 0%;
  }
  @media screen and (max-height: 1024px) and (max-width: 768px){     
    width: 0%;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){     
    width: auto;
    max-height: 65px;
  }    
}
.lineButtonByPhoneDiv{
  padding: 0%;    
  @media screen and (max-height: 823px) and (max-width: 483px){     
    padding: 7%;
  }     
} 
.lineButtonImg{
  width: 6%;
  margin-top: -47%;
  margin-left: 2%;
  position:fixed;
  @media screen and (max-height: 1366px) and (max-width: 1024px){  
    margin-top: -30%;
    width: 6%;
  }
  @media screen and (max-height: 1024px) and (max-width: 768px){     
    width: 6%;
    margin-top: -45%;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){     
    margin-top: 0%;
    width: 0%;
    position: unset;
  }  

}
.phoneButtonImg{
  width: 6%;
  margin-top: -40%;
  margin-left: 2%;
  position:fixed;
  @media screen and (max-height: 1366px) and (max-width: 1024px){  
    margin-top: -20%;
    width: 6%;
  }
  @media screen and (max-height: 1024px) and (max-width: 768px){     
    width: 6%;
    margin-top: -55%;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){     
    margin-top: 0%;
    width: 0%;
    position: unset;
  }    
}
.buttonDiv{
  margin-top: 1%;
  margin-left: 2%;
  margin-right: 2%;
  min-height: auto;
  @media (max-width:1024px){
    margin-left: 0%;
    margin-right: 0%;
  }
  @media (max-width:768px){
    margin-left: 0%;
    margin-right: 0%;
  }     
  @media (max-width:483px) {
    margin-left: 0%;
    margin-right: 0%;
  }   
  @media (max-width:320px) {
    margin-left: 0%;
    margin-right: 0%;
  }    
}

.addLine{
  max-height: auto;
  width:30%;
  @media (max-width:483px) {
    width: 50%;
  } 
}
.header3 {
  font-size: 3.75rem;
  color: #ffffff;
  position:fixed;
  min-height: auto;
  margin-top: -35%;
  @media screen and (max-height: 1366px) and (max-width: 1024px){
    font-size: 3.75rem;
    color: #a7a8a9e0;
    margin-top: 7%;
  }
  @media screen and (max-height: 1024px) and (max-width: 768px){
    position: unset;
    margin-top: 3%;
    font-size: 2.75rem;
    color: #a7a8a9e0;
  }     
  @media screen and (max-height: 823px) and (max-width: 483px){
    font-size: 1.65rem;
    margin-top: -100%;
    color: #a7a8a9e0;
  }     
}
.homeNavCss{
  min-height: auto;
  margin-top: 76px;
  @media (max-width:483px) {
    margin-top: 56px;
  }    
}
.ul {
  list-style: none;
  padding: 0;
}
.li {
  padding-left: 1.3em;
}
.li:before {
  content: "\f00c"; /* FontAwesome Unicode */
  font-family: FontAwesome;
  display: inline-block;
  margin-left: -1.3em; /* same as padding-left set on li */
  width: 1.3em; /* same as padding-left set on li */
}
p {
    display: table-cell;
    align-items: center;
}
</style>
