<template>
  <div id="background">
    <NavgationBar></NavgationBar>
    <Deep></Deep>
    <MoreArticles></MoreArticles>
    <Foot></Foot>
  </div>
</template>

<script>
  import NavgationBar from '../../components/navgationBar/navgationBar.vue'
  import Deep from '../../components/deep/deep.vue'
  import MoreArticles from '../../components/deep/moreArticles.vue'
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
