<template>
  <div>
    <el-container>
      <el-header  class="header">
         <vheader />
      </el-header>
      <el-container  :style="height">
        <el-main>
            <mainContent/>
        </el-main>
      </el-container>
      <el-footer>M-Pay © 2019 Mitena</el-footer>
    </el-container>
  </div>
</template>

<script>
import Header from './Header'
import mainContent from '../components/mainContent'
export default {
  name: 'app',
  components: {
    'vheader': Header,
    mainContent,
  },
  data() {
    return {
      height: {
        height: window.innerHeight - 120 + 'px'
      }
    }
    
  }
}
</script>

<style>

.header {
  background-color: #545c64;
  color: #fff;
  line-height: 80px;
}
.el-footer {
    background-color:gainsboro;
    color: #333;
    line-height: 60px;
  }
.el-main {
    color: #333;
  }
</style>
