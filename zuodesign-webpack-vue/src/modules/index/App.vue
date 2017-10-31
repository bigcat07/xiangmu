<template>
  <div>
    <NavgationBar></NavgationBar>
    <div id="main">
      <div id="left-content">
        <mainContent></mainContent>
        <webHot></webHot>
      </div>
      <div id="right-content">
        <hotRecommend></hotRecommend>
        <reCommend></reCommend>
      </div>
    </div>

  </div>

</template>

<script>
  import MyIndex from '../../components/index/Index'
  import NavgationBar from '../../components/navgationBar/navgationBar.vue'
  import mainContent from '../../components/maincontent/mainContent.vue'
  import hotRecommend from '../../components/hotrecommend/hotRecommend.vue'
  import reCommend from '../../components/recommend/reCommend.vue'
  import webHot from '../../components/webhot/webhot.vue'
  export default {
    name: 'index',
    components: {
        MyIndex,
        NavgationBar,
        mainContent,
        webHot,
        hotRecommend,
        reCommend
    }
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";

  #main {
    width: 880px;
    margin: auto;
    margin-top: 20px;
    overflow: hidden;
  }
  #left-content {
    float: left;
  }
  #right-content {
    float: right;
  }
</style>
