<template>
  <div>
    <p>推荐关注</p>
    <div>
        <div v-for="(val, i) in this.alljson" class="recommend" key="{val}">
            <div class="username">
              <a href="">{{val.username}}</a>
            </div>

            <div class="section">
              <a href="">{{val.section}}</a>
            </div>

            <div class="headimg" @mouseenter="over(i, $event)" >
              <a href="">
                <img :src="val.headimg" :title="val.username">
              </a>
              <div class="mask" @mouseleave="moveOut(i, $event)" @click="link">
              </div>
            </div>
        </div>
    </div>
    <!--下方练习方式-->
    <div id="information">
      <div id="offical">
        <p class="text">下载IOS版 App</p>
        <div class="logo">
          <img src="../../assets/woodpecker1.png" alt="">
        </div>
      </div>
      <div id="wechat">
        <p class="text">关注微信公众号</p>
        <div class="logo">
          <img src="../../assets/weixinPublic.png" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    var mask = document.getElementsByClassName('mask')
    export default {
        name: '',
        data () {
          return {
            usernameArr : [],
            content : [],
            imgArr : [],
            dis : false,
            alljson: []
          }
        },
        methods : {
          over : function (i, ev) {
            if (ev.target.className == 'headimg'){
              mask[i].style.display = 'block'
            }

          },
          moveOut : function (i, ev) {
            if (ev.target.className == 'mask'){
              mask[i].style.display = 'none'
            }
          },
          link : function () {
            window.open('http://www.baidu.com','_self')
          }
        },
        mounted () {
          var _that = this
          axios.get('api/web_reco_users').then(
            function (res) {
              var a = [
                [
                  { username:'',
                    section:'',
                    headimg:''
                  }
                ],
                [
                  { username:'',
                    section:'',
                    headimg:''
                  }
                ],
                [
                  { username:'',
                    section:'',
                    headimg:''
                  }
                ],
                [
                  { username:'',
                    section:'',
                    headimg:''
                  }
                ],
                [
                  { username:'',
                    section:'',
                    headimg:''
                  }
                ],
              ];
                for ( var v in res.data.reco_users) {
                  a[v].username = res.data.reco_users[v].username
                }
                for (var i in res.data.reco_users) {
                  a[i].section = res.data.reco_users[i].introduction
                }
                for (var i in res.data.reco_users) {
                  a[i].headimg = res.data.reco_users[i].avatar
                }
                _that.alljson = a;
            }
          )
        }
    }
</script>

<style scoped>
  .recommend {
    position: relative;
    border-bottom: 1px solid darkgray;
    padding-bottom: 10px;
    padding-top: 10px;
    width: 288px;
  }
  .recommend a {
    text-decoration: none;
  }
  .section {
    margin-top: 6px;
    width: 145px;
  }
  .section>a {
    color: #999eb8;
    font-size: 12px;
  }
  .section>a:hover {
    color: rgb(88,85,87);
  }
  .username>a {
      color: #535557;
      font-size: 16px;
  }
  .username>a:hover {
    color: rgb(154,153,160);
  }
  .headimg {
    position: absolute;
    width: 40px;
    height: 40px;
    left: 250px;
    top: 20px;
  }
  .headimg img {
    width: 40px;
    height: 40px;
    border-radius: 4px;
  }
  .headimg>a {
    height: 40px;
    width: 40px;
  }
  /*蒙版*/
  .mask {
    width: 40px;
    height: 40px;
    background-color: black;
    opacity: 0.6;
    position: absolute;
    left: 0px;
    top: 0px;
    border-radius: 4px;
    display: none;
    cursor: pointer;
  }
  .mask>a {
    width: 100%;
    height: 100%;
  }
  /*练习方式*/
  #information {
    margin-top: 30px;
  }
  #information>div {
    width: 220px;
    height: 50px;
    border: 1px solid rgb(236,236,236);
    background-color: rgb(246,246,246);
  }
  #offical:hover {
    background-color: rgb(251,251,251);
  }
  #offical:hover div {
    content: url("../../assets/woodpecker_hover.png");
    height: 45px;
    border-radius: 4px;
  }
  #wechat:hover {
    background-color: rgb(251,251,251);
  }
  #wechat:hover div {
    content: url("../../assets/weixinPublic_hover.png");
    height: 45px;
    border-radius: 4px;
  }
  #wechat {
    margin-top: 15px;
  }
  .text {
    display: inline-block;
    width: 160px;
    height: 50px;
    line-height: 50px;
    border-right: 1px solid rgb(236,236,236);
    text-align: center;
    font-weight: 500;
  }
  .logo {
    width: 50px;
    height: 50px;
    padding: 4px 7px;
    display: inline-block;
    vertical-align: middle;
  }
  .logo>img {
  border-radius: 4px;
  }

</style>
