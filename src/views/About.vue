<template>
  <div class="about">
    <h2>About</h2>
    <el-row :gutter="20">
      <el-col :span="12">
        <el-divider content-position="left">Quiz Question Maker</el-divider>
        <el-row>
          <el-col :span="4">
            <img src="@/assert/evgwed.jpg" width="100%" class="logo_user" />
          </el-col>
          <el-col :span="18" :offset="2">
            <p>
              <b>Quiz Question Maker (qqMaker)</b> - это система, которая позволяет создавать вопросы для
              <a href="https://xeurun.github.io/quiz-client/" target="_blank">Quiz Client</a>
              в формате JSON.
            </p>
            <p>
              <b>Дата создания: </b> 26 августа 2019 <br>
              <b>Автор: </b> Евгений Прохоров (<a href="https://github.com/evgwed/" target="_blank">@evgwed</a>)
            </p>
          </el-col>
        </el-row>
        <el-divider content-position="left">Quiz Client</el-divider>
        <el-row>
          <el-col :span="4">
            <img src="@/assert/xeurun.png" width="100%" class="logo_user" />
          </el-col>
          <el-col :span="18" :offset="2">
            <p>
              <b>Quiz Client</b> - система для тестирования, которая позволяет загрузить свою базу вопросов и ответов и провести тестирование по ней.
            </p>
            <p>
              <b>Дата создания: </b> 2018 год <br>
              <b>Автор: </b> Алексей Степанков (<a href="https://github.com/xeurun" target="_blank">@xeurun</a>)
            </p>
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="9" :offset="3">
        <img src="@/assert/about-bg.gif" width="100%"/>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
  .logo_user {
    border-radius: 50%;
    box-shadow: 0 0 2px rgba(0, 38, 93, 0.6);
  }
  .about p {
    color: #999;
    font-size: 0.9em;
  }
  .about a {
    color: #006dcc;
  }
</style>
