<template>
  <div>
    <!--放流程icon-->
    <div> 
        <el-row >
            <el-col :span="24">
                <div class="grid-row">
                   <h3>PAYMENT WAY</h3>
                </div>
                <el-row :gutter="10">
                  <el-col :xs="12" :sm="12" :md="6" :lg="6" :xl="6">
                    <div class="grid-content" :class="{'bg-yellow': payMeth === 'superMarket'}">
                      <div @click="payWay('superMarket')"><i class="el-icon-s-shop"></i>超商付款</div>
                    </div>
                  </el-col>
                  <el-col :xs="12" :sm="12" :md="6" :lg="6" :xl="6">
                    <div class="grid-content" :class="{'bg-yellow': payMeth === 'card'}">
                      <div @click="payWay('card')"><i class="el-icon-bank-card"></i>信用卡/金融卡</div>
                    </div>
                  </el-col>
                  <el-col :xs="12" :sm="12" :md="6" :lg="6" :xl="6">
                    <div class="grid-content"  :class="{'bg-yellow': payMeth === 'atm'}">
                      <div @click="payWay('atm')"><i class="el-icon-refresh"></i>ATM轉帳</div>
                    </div>
                  </el-col>
                  <el-col :xs="12" :sm="12" :md="6" :lg="6" :xl="6">
                    <div class="grid-content" :class="{'bg-yellow': payMeth === 'paypal'}">
                      <div @click="payWay('paypal')"><i class="el-icon-s-finance"></i>PayPal</div>
                    </div>
                  </el-col>
                </el-row>
            </el-col>
        </el-row>
        <el-divider><i class="el-icon-bank-card"></i></el-divider>
        <component :is="payMeth" @paybtn="paybtn"></component>
        <el-divider><i class="el-icon-money"></i>付款金額:2,549</el-divider>
        <el-row type="flex" class="row-bg" justify="center">
        <el-col :span="8" :lx="8" :lg="8" :md="8" :sm="24" :xs="24">
            <div style="text-align:center; margin-top:10px;">
              <el-button type="danger" @click="goBack">回購物車</el-button>
                <el-button 
                type="info"
                @click="checkout" 
                :disabled="disabled"
                 v-loading.fullscreen.lock="fullscreenLoading"
                 element-loading-text="Loading , 不要走~~~~!!!"
                >確認付款</el-button>
                <!--點選時切換components-->
            </div>
            </el-col>
        </el-row>
    </div>
  </div>
</template>

<script>
import superMarket from './superMarket'
import card from './card'
import atm from './atm'
import paypal from './paypal'
export default {
components: {
    superMarket,
    card,
    atm,
    paypal
  },
  data(){
    return{
      fullscreenLoading: false,
      payMeth:'superMarket',
      disabled: true,
    }
  },
  methods: {
    goBack(){
        this.$emit('changeCompo','orderList');
    },
    checkout(){
            this.fullscreenLoading = true;
        setTimeout(() => {
          this.fullscreenLoading = false;
           this.$emit('changeCompo','payCompleted');
        }, 3000);
    },
    payWay(val){
      this.payMeth = val;
    },
    paybtn(btnStatus){
      if(btnStatus =='ok'){
        this.disabled = false
      } else {
        this.disabled = true
      }
    },
  },

}
</script>
<style scoped>
  .bg-yellow {
    background: rgb(255, 208, 75);
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: rgb(255, 225, 144);
  }
   .grid-content:hover {
     background: rgb(255, 225, 144);
   }
  .grid-row {
    min-height: 36px;
    height:auto;
    text-align:left;
   }
  .grid-content {
    vertical-align: middle;
    text-align: center;
    border-radius: 5px;
    margin-top:10px;
    line-height:  100px;
    max-width:  100%;
    text-align:  center;
    cursor: pointer;
    border:2px solid rgb(255, 225, 144);
  }

</style>