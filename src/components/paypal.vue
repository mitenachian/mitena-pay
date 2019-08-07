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
            <el-form-item label="卡號" prop="cardNo">
              <el-input v-model="ruleForm.cardNo"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="6" :lg="6" :md="6" :xs="24" :sm="24">
            <el-form-item label="安全碼" prop="cardCode">
              <el-input v-model="ruleForm.cardCode"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="6" :lg="6" :md="6" :xs="24" :sm="24">
            <el-form-item label="到期日" prop="cardDate">
              <el-input v-model="ruleForm.cardDate" placeholder="03/21"></el-input>
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
    ruleForm: {
          name: '',
          email: '',
          cardNo: '',
          cardCode: '',
          cardDate:'',
        },
     rules: {
          name: [
            { required: true, validator: this.checkName, trigger: 'blur' }
          ],
          email: [
            { required: true, type: 'email', message: '請輸入正確email', trigger: 'blur' }
          ],
          cardNo: [
            { required: true, validator: this.checkCardNo, trigger: 'blur' }
          ],
          cardCode: [
            { required: true, validator: this.checkCardCode, trigger: 'blur' }
          ],
          cardDate: [
            { required: true, validator: this.checkCardDate, trigger: 'blur' }
          ]
        }
    }
  },
  methods: {
    checkName(rule, value, callback) {
      if (!!!value) {
        callback(new Error('姓名為必填!'));
      } else {
        if(value.length< 2) {
          callback(new Error('請輸入您的完整姓名!'));
        } else{
          callback();
        }
      }
    },
    checkCardNo(rule, value, callback) {
      if (!!!value) {
        callback(new Error('請輸入卡號'));
      } else {
        if(value.length< 16) {
          callback(new Error('請輸入完整的16碼卡號喔'));
        } else{
          callback();
        }
      }
    },
    checkCardCode(rule, value, callback) {
      if (!!!value) {
        callback(new Error('請輸入安全碼'));
      } else {
        if(value.length !== 3) {
          callback(new Error('請輸入正確的安全碼'));
        } else{
          callback();
        }
      }
    },
    checkCardDate(rule, value, callback) {
      if (!!!value) {
        callback(new Error('請輸入信用卡到期日'));
      } else {
        if(value.length < 4) {
          callback(new Error('請輸入正確的到期日'));
        } else{
          callback();
        }
      }
    },
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