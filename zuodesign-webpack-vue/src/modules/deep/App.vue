<template>
  <div id="background">
    <NavgationBar></NavgationBar>
    <Deep></Deep>
    <MoreArticles></MoreArticles>
    <Foot></Foot>
  </div>
</template>

<script>
  import NavgationBar from '../../components/navgationBar/NavgationBar.vue'
  import Deep from '../../components/deep/Deep.vue'
  import MoreArticles from '../../components/deep/MoreArticles.vue'
  import Foot from '../../components/footer/Foot.vue'

    export default {
        name: 'deep',
        components: {
          NavgationBar,
          Deep,
          MoreArticles,
          Foot
        }
    }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
  #background {
    background-color: rgb(245,245,245);
  }
</style>
