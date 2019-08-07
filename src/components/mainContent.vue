<template>
  <div>
    <!--放流程icon-->
    <div> 
        <el-row >
            <el-col :xs="2" :sm="2" :md="2" :lx="2" :lg="4"><div class="grid-content "></div></el-col>
            <el-col :xs="20" :sm="20" :md="20" :lx="20" :lg="16"><div class="grid-content">
                <el-row :gutter="10">
                    <el-col :xs="8" :sm="8" :md="8" :lx="8" :lg="8" 
                    class="grid-content step" 
                    :class="{'bg-yellow' : view==='orderList'}"
                    >
                        <p v-on:click="changeView('orderList')"><i class="el-icon-goods"></i>確認訂單</p>
                    </el-col>
                    <el-col :xs="8" :sm="8" :md="8" :lx="8" :lg="8" 
                    class="grid-content step"  
                    :class="{'bg-yellow' : view==='payment'}"
                    >
                        <p v-on:click="changeView('payment')"><i class="el-icon-wallet"></i>支付方式</p>
                    </el-col>
                    <el-col :xs="8" :sm="8" :md="8" :lx="8" :lg="8" 
                    class="grid-content step" 
                    :class="{'bg-yellow' : view==='payCompleted'}"
                    >
                        <p v-on:click="changeView('payCompleted')"><i class="el-icon-circle-check"></i>完成支付</p>
                    </el-col>
                </el-row>
            </div>
            </el-col>
            <el-col :xs="2" :sm="2" :md="2" :lx="2" :lg="4"><div class="grid-content "></div></el-col>
        </el-row>
        <el-row  style="margin-top:20xp;">
            <el-col :xs="2" :sm="2" :md="2" :lx="2" :lg="4"><div class="grid-content "></div></el-col>
            <el-col :xs="20" :sm="20" :md="20" :lx="20" :lg="16"><div class="grid-content">
                <component :is="view" @changeCompo="changeCompo"></component>
                <!--訂單資料 componets-->
                <!--付款資料+支付方式 componets-->
                <!--訂單完成 componets-->
            </div>
            </el-col>
            <el-col :xs="2" :sm="2" :md="2" :lx="2" :lg="4"><div class="grid-content "></div></el-col>
        </el-row>
    </div>
  </div>
</template>

<script>

import orderList from './orderList'
import payment from './payment'
import payCompleted from './payCompleted'
export default {
components: {
    orderList,
    payment,
    payCompleted
  },
  data(){
    return{
        view: 'orderList',
    }
  },
  methods: {
      changeCompo(viewName) {
         this.view = viewName;
      },
      changeView(val) {
          this.view = val;
      }
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
    background: #e5e9f2;
  }
  .step {
    cursor: pointer;
  }
 .step:hover {
    background-color:rgb(252, 219, 130);
  }
  .grid-content {
    min-height: 36px;
    height:auto;
    border-radius: 5px;
  }
</style>