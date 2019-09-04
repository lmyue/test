
### 1、index.html
 ```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="renderer" content="webkit">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,Chrome=1" />
    <meta name="renderer" content="webkit" />
    <meta name="viewport" content="initial-scale=1, maximum-scale=1, user-scalable=no, width=device-width">
    <meta name="keywords" content="模板" >
    <meta name="模板" >
    <title>模板</title>
    <link rel="shortcut icon " type="images/x-icon" href="static/favicon.ico">
    
    <!--element-ui相关的可下载到本地，也可以使用cdn-->
    <link rel="stylesheet" href="static/element-ui/2.12.0/theme-chalk/index.css"/>
  </head>
  <style>

  </style>
  <body>
  
     <!-- 因为Element依赖Vue，vue.js需要在element-ui之前引入，所以vue.js也要改为cnd的引入方式-->
    <script src="https://cdn.bootcss.com/vue/2.6.10/vue.min.js"></script>
    <script src="static/element-ui/2.12.0/index.js" charset="utf-8"></script>
    
    <div id="app"></div>
  </body>
</html>
 ```
 
 ### 2、webpack.base.conf
  ```
  module.exports = {
    //...
    externals : {
       'vue': 'Vue',
       'element-ui': 'ElEMENT',
     },
    //...
  }
 ```
### 3、使用
 ```
<template>
  <div>
    <el-button type="danger" @click="test">测试</el-button>
    <el-dialog :visible.sync="visible" title="Hello world">
      <p>Try Element</p>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    data(){
      return{
        visible:false,
      }
    },
    methods:{
      test() {
        this.visible = true;
      },
    }
  }
</script>

<style scoped lang="less">

</style>
 ```
