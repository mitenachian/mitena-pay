<template>
  <div>
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" 
			label-position="center">
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
            <el-form-item label="付款銀行" prop="bank">
                <el-select v-model="ruleForm.bank" placeholder="請選擇銀行" style="width:100%">
                  <el-option
                    v-for="item in bankList"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
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
export default {
  data(){
    return{
      stateChecked: false,
      storeSelect:'',
      ruleForm: {
            name: 'Demo',
            email: 'Demo@example.com',
            bank: '812',
          },
      rules: {
            name: [
              { required: true, message: '請輸入大名', trigger: 'blur' }
            ],
            email: [
              { required: true, type: 'email', message: '請輸入正確email', trigger: 'blur' }
            ],
            bank: [
              { required: true, message: '請選擇付款銀行', trigger: 'blur' }
            ],
          },
      bankList: [
        { value: '812', label: '812-台新銀行'},
        { value: '123', label: '123-玉山銀行'},
        { value: '456', label: '456-合作金庫'},
        { value: '141', label: '141-中國信託'},
        { value: '321', label: '321-國泰世華'},
      ],
    }
  },
  methods: {
    checkForm(formName){
      this.$refs['ruleForm'].validate((valid) => {
          if (valid && this.stateChecked) {
            console.log('valid')
            this.$emit('paybtn','ok');
          } else {
            console.log('no')
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