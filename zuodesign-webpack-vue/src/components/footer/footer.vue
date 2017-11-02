<template>
  <div>
    <div id="mask" v-if="isShow" @click="dbmask"></div>
    <!--关注微信号-->
    <div id="wechat" v-if="isSrc" @click="dbsrc">
      <img src="../../assets/scan-wechat.png" alt="">
    </div>
    <!--意见反馈-->
    <div id="feedback">
      <p>意见反馈</p>
      <div>
        <textarea placeholder="你有啥想ZUO的,快告诉我们呀~~"></textarea>
      </div>
    </div>
    <div id="footer">
        <div id="about">
            <span @click="showmask">关注公众号</span>
          <a href="">关于ZUO</a>
            <span>反馈吐槽</span>
        </div>
        <p>上海设慧网络科技有限公司2016版权所有&nbsp;&nbsp;&nbsp;沪ICP备15013372号</p>
    </div>
  </div>
</template>

<script>
    export default {
        name: '',
        data () {
          return {
            isShow:false,
            isSrc:false
          }
        },
        methods:{
          dbmask:function () {
            this.isShow = false
            this.isSrc = false
          },
          dbsrc:function () {
            this.isShow = false
            this.isSrc = false
          },
          showmask:function () {
            this.isShow = true
            this.isSrc = true
          }
        }
    }
</script>

<style scoped>
  #footer {
    height: 84px;
    background-color: #EAEAEA;
    margin-top: 40px;
  }
  #about {
    width: 240px;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    margin: auto;
    padding-top: 10px;
  }
  #about>a {
    text-decoration: none;
    color: #999A9A;
    font-size: 13px;
  }
  #about>span {
    font-size: 13px;
    color: #999A9A;
    cursor: pointer;
  }
  p {
    width: 380px;
    margin: auto;
    font-size: 13px;
    text-align: center;
    color: #B8B9C4;
    margin-top: 15px;
  }
  #mask {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    z-index: 10;
    background-color: rgba(0,0,0,0.8);
  }
  #wechat {
    width: 440px;
    height: 440px;
    position: absolute;
    left: 50%;
    margin-left: -220px;
    z-index: 13;
    top: 50%;
    margin-top: -220px;
  }
  #wechat>img {
    width: 100%;
    height: 100%;
    border-radius: 4px;
  }
  #feedback {
    position: absolute;
    width: 540px;
    left: 50%;
    margin-left: -270px;
    top: 50%;
    margin-top: -270px;
  }
  #feedback>p {
    height: 74px;
    width: 540px;
    background-color: black;
    color: white;
    font-size: 16px;
    font-weight: 600;
    text-align: center;
    line-height: 74px;
  }
  #feedback>div {
    width: 540px;
    background-color: white;
    height: 316px;
    margin: auto;
    padding-top: 20px;
  }
  textarea {
    width: 488px;
    height: 186px;
    margin: auto;
    resize: none;
    border: none;
    outline: none;
    font-size: 14px;
    padding: 10px;
    background-color: #F6F6F6;
  }
</style>
