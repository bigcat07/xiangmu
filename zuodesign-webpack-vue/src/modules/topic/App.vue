<template>
  <div class="background">
    <NavgationBar></NavgationBar>
    <div id="content">
      <div id="left">
        <MainContentII></MainContentII>
        <HotComments></HotComments>
        <Comments></Comments>
      </div>
      <div id="right">
        <Publish></Publish>
      </div>
    </div>
    <Foot></Foot>
  </div>
</template>

<script>
    import NavgationBar from '../../components/navgationBar/NavgationBar.vue'
    import MainContentII from '../../components/maincontent/MainContentII.vue'
    import HotComments from '../../components/maincontent/HotComments.vue'
    import Comments from '../../components/maincontent/Comments.vue'
    import Publish from '../../components/maincontent/Publish'
    import Foot from '../../components/footer/Foot.vue'
    export default {
        name: '',
        components:{
          NavgationBar,
          MainContentII,
          HotComments,
          Comments,
          Publish,
          Foot
        }
    }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
  .background {
    background-color: rgb(245,245,245);
  }
  #content {
    width: 840px;
    margin: auto;
    overflow: hidden;
    margin-top: 20px;
  }
  #left {
    float: left;
  }
  #right {
    float: right;
    width: 240px;
  }
</style>
