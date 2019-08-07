<template>
  <div>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" 
			label-position="center" >
        <el-row>
          <el-col :span="12" :lg="12" :md="12" :xs="24" :sm="24">
            <el-form-item label="訂購人" prop="name">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12" :lg="12" :md="12" :xs="24" :sm="24">
            <el-form-item label="Email" prop="email">
              <el-input v-model="ruleForm.email"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12" :lg="12" :md="12" :xs="24" :sm="24">
            <el-form-item label="超商" prop="store">
                <el-select v-model="ruleForm.store" placeholder="請選擇超商" style="width:100%">
                  <el-option
                    v-for="item in storeList"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="12" :lg="12" :md="12" :xs="24" :sm="24">
            <el-form-item label="分店代號" prop="storeNo">
              <el-input v-model="ruleForm.storeNo"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="24" :lg="24" :md="24" :xs="24" :sm="24">
            <el-checkbox  v-model="stateChecked" @change="checkForm('ruleForm')">Yes</el-checkbox>
             <span style="word-wrap:break-word;">．我已詳知<el-link type="danger">相關條款</el-link>,M-Pay將依您提供資料與銀行照會及保留出貨權益，提醒您勿冒用他人個資進行交易，經查獲必移送法辦</span>
          </el-col>
        </el-row>
      </el-form>
  </div>
</template>

<script>
import { truncateSync } from 'fs';
export default {
  data(){
    return{
      stateChecked: false,
      storeSelect:'',
      ruleForm: {
            name: 'Demo',
            email: 'demo@demo.com',
            store: '7-11',
            storeNo:'711-098',
          },
      rules: {
            name: [
              { required: true, message: '請輸入您的完整姓名', trigger: 'blur' }
            ],
            email: [
              { required: true, type: 'email', message: '請輸入正確email', trigger: 'blur' }
            ],
            store: [
              { required: true, message: '請選擇商店', trigger: 'blur' }
            ],
            storeNo: [
              { required: true, message: '請輸入分店代號', trigger: 'blur' }
            ],
          },
      storeList: [
        { value: '7-11', label: '7-11'},
        { value: '全家便利商店', label: '全家便利商店'},
        { value: '萊爾富', label: '萊爾富'},
        { value: 'OK Mart', label: 'OK Mart'},
      ],
    }
  },
  methods: {

    checkForm(formName){
          this.$refs['ruleForm'].validate((valid) => {
          if (valid && this.stateChecked) {
            this.$emit('paybtn','ok');
          } else {
            this.stateChecked = false;
            this.$emit('paybtn','no');
            return false;
          }
        });

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