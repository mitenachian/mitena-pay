<template>
  <div>
    <!--放流程icon-->
    <div> 
        <el-row >
            <el-col :span="24">
                <div class="grid-content">
                   <h3>OREDER COMPLETED</h3>
                </div>
                <img alt="Vue logo" src="../assets/paymentEnd.png">
            </el-col>
        </el-row>
        <el-divider><i class="el-icon-success"></i>感謝您的購買,我們將盡快為您安排出貨</el-divider>
        <el-row type="flex" class="row-bg" justify="center">
        <el-col :span="8" :lx="8" :lg="8" :md="8" :sm="24" :xs="24">
            <div style="text-align: center; margin-top:10px;">
                <el-button type="info" @click="checkout">進度查詢</el-button>
                <!--點選時切換components-->
            </div>
        </el-col>
        </el-row>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
    }
  },
  methods: {
    checkout(){
       this.$alert('這個訂單不出貨 (´;ω;`)', '告訴你一個壞消息', {
          confirmButtonText: '哭哭',
          callback: action => {
            this.$message({
              type: 'info',
              message: `action: ${ action }`
            });
          }
        });
    }
  },
  computed: {
	countTotal:function(){
		var countTotal=0;
		for (var i in this.orders) {
			countTotal += parseInt(this.orders[i].qty*this.orders[i].specialPrice);
		}
		return countTotal;
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
  .grid-content {
    min-height: 36px;
    vertical-align: middle;
    height:auto;
    line-height: 50px;
    text-align: left;
  }
  .rigth {
     text-align: right;
  }
  .inlineDiv {
      display:inline-block;
      margin-right:20px;
  }
</style>