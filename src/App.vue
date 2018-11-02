<template>
  <div id="app">
      <div class="left">
        <leftVue class='left-Vue'></leftVue>
      </div>
      <div><router-view/></div>
  </div>
</template>

<script>
import leftVue from"@/components/leftVue"

  export default {
    name: 'App',
    components:{
      leftVue
    }
  }
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    height: 100%;
  }
  .left{
    height: 100%;
    float: left;
  }
  .left-Vue{
        width: 100px;
        height: 100%;
        background: #77ccdd;
  }
  .left-Vue li{
    list-style: none;
    color:#fff;
    text-align:center;
    height: 100px;
    padding-top:20px; 
    border-bottom: 1px solid #fff;
  }
  .iconfont{
    font-size: 24px;
  }
</style>
