<template>
  <el-row>
    <el-col :span="24">
        <div class="head-wrap">
            <img alt="Vue logo" src="../assets/logo.png" style="width:70px; margin:5px;">
        </div>
    </el-col>
  </el-row>
</template>
<script>
export default {
  methods: {
    singOut(){  
      console.log('logOut!')
    }
  },
}
</script>
<style scoped>
	.right-menu {
		float: right;
		height: 100%;

  }
	.right-menu-item {
			display: inline-block;
			margin: 0 8px;
      color:aliceblue;
		}
</style>