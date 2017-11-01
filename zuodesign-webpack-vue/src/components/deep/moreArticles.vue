<template>
  <div id="background">
    <h4>更多文章</h4>
    <div id="mainContent">
      <div v-for="(v,i) in array" class="articles" @mouseenter="over(i)" @mouseleave="out(i)">
        <!--图片-->
        <div class="picture">
          <a href="#">
            <img :src="v.banner" alt="">
          </a>
        </div>
        <!--描述-->
        <p class="title">
          <a href="#">{{v.title}}</a>
        </p>
        <!--下方作者和时间-->
        <div class="footer">
          <p class="author">{{v.author.name}}</p>
          <p class="time">{{v.timeAgo}}</p>
        </div>
      </div>
    </div>
    <div id="anchorPoint">
      <a href="#nav">
        <img src="../../assets/up.png" alt="">
      </a>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    var articles = document.getElementsByClassName('articles')
    export default {
        name: '',
        data () {
          return {
            array:[]
          }
        },
        methods:{
          over:function (i) {
            articles[i].style.boxShadow = '5px 5px 3px #E6E6E6'
          },
          out:function (i) {
            articles[i].style.boxShadow = '0px,0px,0px #F6F6F6'
          }
        },
        mounted () {
          var _that = this
          axios.get('api/articles').then(
            function (res) {
              _that.array = res.data.articles
            }
          )
        }
    }
</script>
<style scoped>
  #background {
    background-color: rgb(245,245,245);
    padding-top: 20px;
  }
  h4 {
    width: 100px;
    margin: auto;
    margin-bottom: 10px;
    text-align: center;
    font-weight: 600;
  }
  #mainContent {
    width: 960px;
    margin: auto;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  #mainContent>div {
    width: 218px;
    height: 315px;
    margin-top: 20px;
    position: relative;
    background-color: rgb(255,255,255);
  }
  /*图片*/
  .picture {
    width: 218px;
    height: 160px;
    overflow: hidden;
  }
  .picture img {
    border-radius: 6px;
  }
  /*描述*/
  .title {
    width: 180px;
    margin: auto;
    margin-top: 10px;
  }
  .title>a {
    text-decoration: none;
    color: rgb(38,45,47);
    font-size: 14px;
  }
  .footer {
    position: absolute;
    width: 180px;
    bottom: 5px;
    overflow: hidden;
    left: 20px;
  }
  .footer>p:nth-child(1) {
    float: left;
    font-size: 12px;
  }
  .footer>p:nth-child(2) {
    float: right;
    font-size: 12px;
  }
  /*锚点*/
  #anchorPoint {
    position: fixed;
    right: 50px;
    bottom: 100px;
    width: 40px;
    height: 40px;
    background-color: #A3A6A6;
    border-radius: 4px;
    padding-top: 10px;
    cursor: pointer;
  }
  #anchorPoint>a {
   margin-left: 12px;
  }
</style>
