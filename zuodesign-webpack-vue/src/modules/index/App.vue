<template>
  <div id="background">
    <NavgationBar></NavgationBar>
    <div id="main">
      <div id="left-content">
        <MainContent></MainContent>
        <WebHot></WebHot>
        <HotPosts></HotPosts>
      </div>
      <div id="right-content">
        <HotRecommend></HotRecommend>
        <ReCommend></ReCommend>
      </div>
    </div>

  </div>

</template>

<script>
  import MyIndex from '../../components/index/Index'
  import NavgationBar from '../../components/navgationBar/navgationBar.vue'
  import MainContent from '../../components/maincontent/mainContent.vue'
  import HotRecommend from '../../components/hotrecommend/hotRecommend.vue'
  import ReCommend from '../../components/recommend/reCommend.vue'
  import WebHot from '../../components/webhot/webhot.vue'
  import HotPosts from '../../components/hotPosts/hotPosts.vue'
  export default {
    name: 'index',
    components: {
        MyIndex,
        NavgationBar,
        MainContent,
        WebHot,
        HotRecommend,
        ReCommend,
        HotPosts
    }
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
  #background {
    background-color: rgb(245,245,245);
  }
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
