<template>
  <div>
    <!--放流程icon-->
    <div> 
        <el-row >
            <el-col :span="24">
                <div class="grid-content">
                   <h3>YOUR ORDER ITEM</h3>
                </div>
                <div v-for="( item, index) in orders" :key="index">
                <el-row>
                    <el-col :xs="24" :sm="24" :md="24" class="grid-content ">
                      <div style="float:left;">
                      <el-image :src="image(item.picSrc)" style="width:50px;height:50px"/>
                        <div class="inlineDiv">{{item.prdName}}</div>
                      </div>
                        <div style="float:right;">
                            <div class="inlineDiv" >
                                <el-input-number size="mini" v-model="item.qty" disabled></el-input-number>
                            </div>
                            
                            <div class="inlineDiv">
                                {{item.specialPrice}}
                                <span style="text-decoration:line-through;color:#d4d4d4;font-size:10px;">({{item.price}})</span>
                            </div>
                            <div class="inlineDiv" style="width:30px;">{{item.specialPrice *item.qty}}</div>
                            <div class="inlineDiv"><i class="el-icon-delete"></i></div>
                        </div>
                    </el-col>
                </el-row>
                </div>
            </el-col>
        </el-row>
        <el-divider><i class="el-icon-s-claim"></i></el-divider>
        <el-row type="flex" class="row-bg" justify="end">
        <el-col :span="8" :lx="8" :lg="8" :md="8" :sm="24" :xs="24">
            <div style="text-align: right;">
                結帳金額: {{ countTotal  }}
            </div>
            <div style="text-align: right; margin-top:10px;">
                <el-button type="danger">繼續買</el-button>
                <el-button type="info" @click="checkout">來去結帳</el-button>
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
        orders:[{
            picSrc: 'prd1.jpg',
            prdName: '婚紗酒杯 | 香檳杯 敬酒杯 結婚',
            price: 980,
            specialPrice: 880,
            qty:2,
            },
            {
            picSrc: 'prd2.jpg',
            prdName: '星期天 | 生活中平凡無比的日常',
            price: 999,
            specialPrice: 789,
            qty:1,
            }]
    }
  },
  methods: {
    image(src) {
      return require(`../assets/${src}`);
    },
    checkout(){
        this.$emit('changeCompo','payment');
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
      vertical-align: middle;
      padding:5px;
  }
  .el-image{
    overflow:initial;
  }
</style>