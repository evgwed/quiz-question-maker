<template>
  <div class="app">
    <el-container>
      <el-header>
        <Header />
      </el-header>
      <el-main>
        <router-view/>
      </el-main>
    </el-container>
  </div>
</template>

<script>
  import Header from './components/Header'

  export default {
      components: {
          Header
      }
  }
</script>
<style>
  .app {
    font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  }
</style>
