<template>
  <div id="background">
    <div id="topic">
      <div id="mask">
        <a href="#"></a>
      </div>
      <p id="topic-title">话题</p>
      <p id="line"></p>
      <a href="">
        <img  :src="this.src" alt="">
      </a>
      <p id="headline">
        <a href="">
          {{this.topic}}
          <img src="../../assets/right.png" alt="">
        </a>
      </p>
      <div id="replycount">
        <a href="">
            {{this.people}}人收藏&nbsp&nbsp&nbsp|&nbsp&nbsp&nbsp{{this.reply}}个讨论
        </a>
      </div>
    </div>
    <!--评论-->
    <div id="discuss">
        <p v-if="this.usernameArr.length > 0">
          <a href="#">
            {{this.usernameArr[index].author.username}}:
            <span>{{this.usernameArr[index].text}}</span>
          </a>

        </p>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: '',
        data () {
          return {
            topic : '',
            src : '',
            people : 0,
            reply : 0,
            usernameArr: [],
            index:0,
          }
        },
        methods:{

        },
        mounted() {
          var _that = this;
          setInterval(function () {
            _that.index++
            if (_that.index == 5) {
              _that.index = 0
            }
          },4000)
          axios.get('api/topics').then(
            function (res) {
              _that.topic = res.data.topic.title
              _that.src = res.data.topic.cover
              _that.people = res.data.topic.collect_count
              _that.reply = res.data.topic.comment_count
              _that.usernameArr = res.data.topic.comments
            }
          )
        }
    }
</script>

<style scoped>
  #topic {
    width: 540px;
    height: 180px;
    position: relative;
  }
  #mask {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: black;
    opacity: 0.3;
    /*cursor: pointer;*/
  }
  #mask>a {
    display: inline-block;
    width: 100%;
    height: 100%;
  }
  /*话题*/
  #topic-title {
    position: absolute;
    color: white;
    font-weight: bold;
    font-size: 14px;
    left: 30px;
    top: 20px;
  }
  #line {
    height: 6px;
    width: 20px;
    background-color: rgb(255,209,88);
    position: absolute;
    border-radius: 4px;
    left: 30px;
    top: 50px;
  }

  /*标题*/
  #headline {
    position: absolute;
    left: 30px;
    top: 100px;
  }
  #headline>a {
    text-decoration: none;
    color: white;
    font-size: 20px;
  }
  /*评论回复*/
  #replycount {
    position: absolute;
    top: 140px;
    left: 30px;
  }
  #replycount>a {
    text-decoration: none;
    color: rgb(193,185,177);
    font-size: 14px;

  }
  #headline>a {
    vertical-align: bottom;
  }
  #headline>a>img {
    width: 20px;
  }
  #discuss {
    width: 540px;
    height: 80px;
    background-color: white;
    padding-top: 20px;
    padding-left: 20px;
  }
  #discuss>p>a {
    font-size: 13px;
    color: #262D2F;
    word-wrap : break-word;
  }
  #discuss a {
    text-decoration: none;
  }
  #discuss>p>a>span {
    font-size: 13px;
    color: #999A9A;
  }
</style>
