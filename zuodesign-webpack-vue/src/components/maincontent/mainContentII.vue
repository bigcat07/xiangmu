<template>
  <div>
    <div id="out">
      <p id="topic">话题</p>
      <p id="line"></p>
      <p id="title">{{topic.title}}</p>
      <p id="time">发布于{{topic.timeAgo}}&nbsp;&nbsp;|&nbsp;&nbsp;已有{{topic.collect_count}}人收藏</p>
      <div>
        <img :src="topic.cover" alt="">
      </div>
      <p v-html="topic.content"></p>
      <div id="collect">
        <div>
          <img src="../../assets/star.png" alt="">
          <span>收藏该话题</span>
        </div>
      </div>
    </div>
    <!--评论-->
    <p id="aboutCount">{{topic.comment_count}}个评论</p>
  </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: '',
        data() {
          return {
            topic:{}
          }
        },
        mounted() {
          var _that = this;
          axios.get('api/topic/575bb18e6be3ff0069503da2').then(
            function (res) {
              _that.topic = res.data.topic
            }
          )
        }
    }
</script>

<style scoped>
  #out {
    width: 540px;
    background-color: white;
    padding-top: 30px;
    padding-left: 20px;
    padding-right: 20px;
    padding-bottom: 20px;
  }
  #topic {
    font-size: 14px;
    font-weight: 500;
  }
  /*分割线*/
  #line {
    width: 20px;
    height: 6px;
    background-color: #FFD158;
    border-radius: 4px;
    margin-top: -10px;
  }
  #title {
    font-size: 22px;
  }
  #time {
    font-size: 12px;
    color: #A9AAAA;
  }
  #collect {
    overflow: hidden;

  }
  #collect>div {
    float: right;
  }
  #aboutCount {
    font-size: 14px;
    color: #303638;
    margin-top: 30px;
    font-weight: 500;
  }
</style>
