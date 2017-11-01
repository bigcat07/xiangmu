<template>
  <div id="background">
    <h4>推荐阅读</h4>
    <div id="title">
      <div v-for="(k,i) in this.titleArray" class="title-content" @mouseenter="over(i)" @mouseleave="out(i)">
        <a href="#">
          <img :src="k.banner" alt="">
        </a>
        <!--大标题-->
        <p class="title">
          <a href="#">{{k.title}}</a>
        </p>
        <!--小标题-->
        <p class="subtitle">
          <a href="#">{{k.summary}}</a>
        </p>
        <!--分割线-->
        <p class="line"></p>
        <div class="tagname">
          <!--圆球-->
          <div class="ball" :style="{backgroundColor:k.sceneTagColor}"></div>
          <a href="#">{{k.sceneTagName}}</a>
        </div>
        <div class="time">
          <a href="#">{{k.timeAgo}}</a>
        </div>
        <!--蒙版-->
        <div class="mask-bottom">

        </div>
        <!--第二层蒙版-->
        <div class="masktop" @click="link">

        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    var mask = document.getElementsByClassName('masktop')
    function getparam() {
      var c1 = window.location.href.split('?')[1];
      var c2 = c1.split('=')[1]
      return c2
    }
    var c = getparam()
    console.log(c)


    export default {
        name: '',
        data () {
          return {
            titleArray:[],
          }
        },
        methods : {
          over:function (i) {
            mask[i].style.display = 'block'
          },
          out:function (i) {
            mask[i].style.display = 'none'
          },
          link:function () {
            window.open('http://www.baidu.com','_self')
          },
          getQueryString:function (name) {
            var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)")
            var r = window.location.search.substr(1).match(reg)
            if (r!=null) {
              return decodeURI (r[2])
            }else {
              return null
            }
          }
        },
        mounted () {
          var _that = this
          axios.get('api/hot_articles').then(
            function (res) {
              for (var i in res.data.hot_articles) {
                _that.titleArray.push(res.data.hot_articles[i])
              }
//              console.log(_that.titleArray[0].summary)
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
    margin-bottom: 30px;
    text-align: center;
    font-weight: 600;
  }
  /*推荐阅读*/
  #title {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 960px;
    margin: auto;
  }
  .title-content {
    width: 300px;
    height: 460px;
    position: relative;
  }
  /*第一层蒙版*/
  .mask-bottom {
    position: absolute;
    left: 0;
    top: 0;
    width: 300px;
    height: 460px;
    border-radius: 6px;
    background-color: black;
    z-index: 10;
    opacity: 0.2;
  }
  /*第二层蒙版*/
  .masktop {
    position: absolute;
    left: 0;
    top: 0;
    width: 300px;
    height: 460px;
    border-radius: 6px;
    background-color: black;
    z-index: 15;
    opacity: 0.4;
    display: none;
    cursor: pointer;
    -webkit-transition: display 2s;
  }
  /*推荐阅读图片*/
  .title-content img {
    width: 100%;
    height: 100%;
    border-radius: 6px;
  }
  .title {
    position: absolute;
    bottom: 120px;
    width: 240px;
    left: 50%;
    margin-left: -120px;
    z-index: 50;
  }
  .title>a {
    text-decoration: none;
    color: white;
    font-size: 18px;
    font-weight: 500;
  }
  /*小标题*/
  .subtitle {
    width: 240px;
    margin-top: 20px;
    position: absolute;
    bottom: 60px;
    left: 50%;
    margin-left: -120px;
    z-index: 50;
  }
  .subtitle>a {
    text-decoration: none;
    color: rgb(226,226,226);
    font-size: 14px;
    z-index: 50;
  }
  /*分割线*/
  .line {
    position: absolute;
    width: 280px;
    height: 1px;
    background-color: rgb(110,108,107);
    left: 50%;
    margin-left: -140px;
    bottom: 30px;
    z-index: 50;
  }
  /*类型*/
  .tagname {
    position: absolute;
    left: 20px;
    bottom: 10px;
    z-index: 50;
  }
  .tagname>a {
    color: rgb(208,208,208);
    text-decoration: none;
    vertical-align: middle;
    font-size: 14px;
    font-weight: 500;
    z-index: 50;
  }
  /*小球*/
  .ball {
    display: inline-block;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    margin-right: 8px;
    z-index: 50;
  }
  .time {
    position: absolute;
    left: 190px;
    bottom: 10px;
    width: 160px;
    z-index: 50;
  }
  .time>a {
    text-decoration: none;
    color: white;
    font-size: 13px;
    z-index: 50;
  }
</style>
