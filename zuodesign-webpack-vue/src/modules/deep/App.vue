<template>
  <div>
    <NavgationBar></NavgationBar>
    <Deep></Deep>
    <MoreArticles></MoreArticles>
  </div>
</template>

<script>
  import NavgationBar from '../../components/navgationBar/navgationBar.vue'
  import Deep from '../../components/deep/deep.vue'
  import MoreArticles from '../../components/deep/moreArticles.vue'
    export default {
        name: 'deep',
        components: {
          NavgationBar,
          Deep,
          MoreArticles
        }
    }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
</style>
