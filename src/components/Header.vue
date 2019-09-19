<template>
  <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" :router="true" >
    <el-menu-item>
      <div class="logotype">
        <img src="@/assert/logo.png">
        <span>
          <span>qq</span>Maker
        </span>
      </div>
    </el-menu-item>
    <el-menu-item index="1" :route="{name: 'home'}">
      <i class="el-icon-brush"></i>
      Quiz Question Maker
    </el-menu-item>
    <el-menu-item index="2" :route="{name: 'about'}">
      <i class="el-icon-bangzhu"></i>
      About
    </el-menu-item>
    <el-menu-item index="4" :route="{name: 'mocky'}" class="mokery_link">
      <i class="el-icon-guide"></i>
      Mocky.io
    </el-menu-item>
    <el-menu-item index="3" :route="{name: 'quiz-client'}" class="quiz_client_link">
      <i class="el-icon-pear"></i>
      Quiz Client
    </el-menu-item>
  </el-menu>
</template>

<script>
export default {
    data() {
        return {
            activeIndex: "1"
        }
    }
}
</script>

<style scoped>
  .mokery_link,
  .mokery_link i {
    color: #006dcc !important;
    text-decoration: none;
  }
  .quiz_client_link,
  .quiz_client_link i {
    color: #283593 !important;
    text-decoration: none;
  }
  .logotype {
    margin-right: 120px;
  }
  .logotype img{
    height: 40px;
  }
  .logotype span{
    margin-left: 10px;
    font-size: 1.5em;
  }
  .logotype span>span{
    color: #49ccc7;
    font-size: 1em;
  }
</style>
