<template>
  <div>
    <div id="nav">
      <div>
        <div id="nav-lianjie">
          <a href="index.html">
            ZUO
            <span>HONEY WASABI</span>
          </a>
        </div>
        <!--中间内容-->
        <div id="nav-title">
          <ul>
            <li v-for="(v,i) in titlearray">
              <a :href="v.url" class="dh" @click="tabClass(i)">{{v.name}}</a>
            </li>

            <li @click="reveal">
              <span style="color: #9DA0A4;font-size: 14px;cursor: pointer">下载APP</span>
            </li>
          </ul>
          <div id="nav-search">
            <input type="text" placeholder="请输入关键字搜索" @keyup.13="plut" v-model="input" ref="input">
            <a id="bigglass" @click="sousuo">
              <img src="../../assets/big.png" alt="" width="22px" height="20px
">
            </a>
          </div>
        </div>
        <!--右侧注册登录-->
        <div id="nav-right-login">
          <ul>
            <li>
              <a href="#" @click="showlogin">登录</a>
            </li>
            <li>
              <a href="#" @click="showregister">注册</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!--导航栏下方内容-->
    <div id="nav-bottom" v-if="isShow">
        <h3>可能是全宇宙最ZUO的图片社区</h3>
        <span @click="isShow = !isShow">X</span>
        <p>
          和像你一样认真对待生活的人一起<br/>
          从设计的视角，重新认识世界
        </p>
        <button type="button" @click="showregister">创建ZUO账号</button>
    </div>

    <!--登录注册蒙版-->
    <div id="mask" v-show="ismask" @click="maskcontrol">

    </div>
    <!--登录-->
    <div id="login" class="lore" v-show="istablogin">
      <p>
        <img src="../../assets/woodpecker.png" width="30px">
        <span>欢迎回到ZUO</span>
      </p>
      <div id="wechat" class="sina">
        <a href="">
          <img src="../../assets/sina.png" alt="">
        </a>
        <a href="">
          <img src="../../assets/WeChat.png" alt="">
        </a>
        <p>你可以使用第三方社交账号直接登录</p>
        <div class="line"></div>
        <div class="or">或者</div>
        <div class="line"></div>
      </div>
      <input type="text" placeholder="手机号" class="ipt">
      <input type="password" placeholder="验证码" class="ipt">
      <button class="yanzhengma">发送验证码</button>
      <div class="noaccount">
        <a href="#" @click="tabregister">没有账号?去注册</a>
        <a href="#" @click="tabyanzhengma">手机密码登录</a>
      </div>
      <button id="login-btn" class="lrbtn">登录</button>
      <div class="close" @click="closemask">X</div>
    </div>
    <!--注册-->
    <div id="register" class="lore" v-show="istabregister">
      <p>
        <img src="../../assets/woodpecker.png" width="30px">
        <span>ZUO  欢迎你的加入</span>
      </p>
      <!--第三方社交-->
      <div class="sina">
        <a href="">
          <img src="../../assets/sina.png" alt="">
        </a>
        <a href="">
          <img src="../../assets/WeChat.png" alt="">
        </a>
        <p>你可以使用第三方社交账号直接登录</p>
        <div class="line"></div>
        <div class="or">或者</div>
        <div class="line"></div>
      </div>
      <!--下方注册-->
      <input type="text" placeholder="手机号" class="ipt">
      <input type="password" placeholder="验证码" class="ipt">
      <button class="yanzhengma">发送验证码</button>
      <input type="password" class="ipt" placeholder="密码">
      <input type="password" class="ipt" placeholder="确认密码">
      <div id="agreement">
        <p>
          <input type="checkbox" @click="isChecked" ref="jiancha" checked="checked">
          <span>
            我已经认真阅读并同意ZUO的用户协议
            <a href="http://zuoooodesign.lofter.com/post/1d1a2c6b_6478482">《用户协议》</a>
          </span>
        </p>
        <a href="#" @click="tablogin">已有账号,登录</a>
      </div>
      <button class="lrbtn" type="button" ref="register" >注册账号</button>
      <div class="close" @click="closemask">X</div>
    </div>
    <!--下载APP-->
    <div id="app" @click="scan" v-show="isApp">
      <img src="../../assets/scan.png" alt="">
    </div>
    <!--手机验证码登录-->
    <div class="lore" v-show="issecurity">
      <p>
        <img src="../../assets/woodpecker.png" width="30px">
        <span>欢迎回到ZUO</span>
      </p>
      <div class="sina">
        <a href="">
          <img src="../../assets/sina.png" alt="">
        </a>
        <a href="">
          <img src="../../assets/WeChat.png" alt="">
        </a>
        <p>你可以使用第三方社交账号直接登录</p>
        <div class="line"></div>
        <div class="or">或者</div>
        <div class="line"></div>
      </div>
      <input type="text" placeholder="手机号" class="ipt">
      <input type="password" placeholder="验证码" class="ipt">
      <div class="noaccount">
        <a href="#" @click="forgetPassword">忘记密码?</a>
        <a href="#" @click="security">手机验证码登录</a>
      </div>
      <button class="lrbtn">登录</button>
      <div class="close" @click="closemask">X</div>
    </div>
    <!--忘记密码-->
    <div class="lore" v-show="isPassword">
      <p id="forgetPassword">
       忘记密码
      </p>
      <input type="text" class="ipt" placeholder="手机号">
      <input type="text" class="ipt" placeholder="验证码">
      <input type="password" class="ipt" placeholder="新密码">
      <input type="password" class="ipt" placeholder="确认新密码">
      <button class="authCode">发送验证码</button>
      <button class="lrbtn">确认修改</button>
      <div class="close" @click="closemask">X</div>
    </div>
    <!--锚点-->
    <div id="up">
      <a href="#">
        <img src="../../assets/up.png" alt="">
      </a>
    </div>
  </div>

</template>

<script>
    var url = window.location.href.split('?')[1]
    var tf = true;
    if (window.history.length == 1) {
      tf = true
    }else {
      if (url != undefined){
        if (url.split('=')[0] == 'id') {
          tf = true
        }else {
          tf = false
        }
      }else {
        tf = false
      }
    }

    export default {
        name: '',
        data () {
          return {
            input:'',
            isShow:tf,
            istablogin : false,
            istabregister:false,
            ismask : false,
            issecurity : false,
            isPassword : false,
            titlearray : [
              {name:'首页',url:'index.html?id=1'},
              {name:'深度',url:'deep.html'}
            ],
            isCC:tf,
            iscur:0,
            isApp:false,
          }
        },
        methods:{
          plut:function () {
            if (this.$refs.input.value == '' || this.$refs.input.value == ' ') {
              alert('请输入搜索内容')
              return false
            }
            window.location.href = 'search.html?name='+this.input
          },
          sousuo:function () {
            if (this.$refs.input.value == '' || this.$refs.input.value == ' ') {
              alert('请输入搜索内容')
              return false
            }
            window.location.href = 'search.html?name='+this.input
          },
//          下载app
          reveal:function () {
            this.ismask = true
            this.isApp = true
          },
          scan:function () {
            this.isApp = false
            this.ismask = false
          },
//         控制蒙版
          maskcontrol:function () {
            this.ismask = false
            this.isApp = false
            this.issecurity = false
            this.isPassword = false
            this.istabregister = false
            this.istablogin = false
          },
          isChecked:function () {
            if(this.$refs.jiancha.checked) {
                this.$refs.register.removeAttribute('disabled')
                this.$refs.register.style.backgroundColor = 'rgb(0,218,224)'
            }else {
              this.$refs.register.style.backgroundColor = 'rgb(153,240,243)'
              this.$refs.register.setAttribute('disabled','false')
              this.$refs.register.style.color = 'rgb(255,255,255)'
            }
          },
          tablogin:function () {
            this.istablogin = true
            this.istabregister = false
          },
          tabregister:function () {
            this.istablogin = false
            this.istabregister = true
          },
          closemask:function () {
            this.ismask = false
            this.istablogin = false
            this.istabregister = false
            this.issecurity = false
            this.isPassword = false
          },
          showlogin:function () {
            this.ismask = true
            this.istablogin = true
          },
          showregister:function () {
            this.ismask = true
            this.istabregister = true
          },
          tabyanzhengma:function () {
            this.issecurity = true
            this.istablogin = false
          },
          security:function () {
            this.issecurity = false
            this.istablogin = true
          },
//          忘记密码
          forgetPassword:function () {
            this.issecurity = false
            this.isPassword = true
          }
        }
    }
</script>

<style scoped>
  #nav {
    background-color: rgb(38,45,47);
    height: 60px;
    position: relative;
  }
  #nav-lianjie {
    display: inline-block;
  }
  #nav-lianjie>a {
    color: white;
    text-decoration: none;
    font-size: 22px;
    font-weight: bold;
    display: inline-block;
    padding: 14px 28px;
  }
  #nav-lianjie>a>span {
    font-size: 12px;
    color: rgb(85,98,108);
  }

  /*中间的标题内容*/
  #nav-title {
    display: inline-block;
    margin-left: 20%;
  }
  #nav-title>ul {
    display: inline-block;
  }
  #nav-title>ul>li {
    display: inline-block;
    margin-right: 30px;
  }
  #nav-title>ul>li>a {
    text-decoration: none;
    color: rgb(157,160,164);
    font-size: 14px;
  }
  /*鼠标链接*/
  /*#nav-title>ul>li:nth-child(1)>a {*/
    /*color: white;*/
  /*}*/
  #nav-search {
    display: inline-block;
    position: relative;
    vertical-align: middle;
  }
  #nav-search>input {
    outline:none;
    padding-left: 10px;
    width: 170px;
    height: 30px;
    border-radius: 6px;
    background-color: rgb(69,76,77);
    border:none;
    font-size: 14px;
    color: white;
  }
  /*搜索放大镜*/
  #bigglass {
    position: absolute;
    right: 5px;
    top: 5px;
  }
  /*右侧登录注册*/
  #nav-right-login {
    display: inline-block;
    position: absolute;
    left: 80%;
    top: 30%;
  }
  #nav-right-login>ul>li {
    display: inline-block;
    margin-right: 15px;
  }
  #nav-right-login>ul>li>a {
    text-decoration: none;
    color: rgb(157,160,164);
    font-size: 14px;
  }
  #nav-right-login>ul>li:nth-child(1) {
    padding-left: 20px;
    background: url("../../assets/login.png") no-repeat 0 3px;
  }
  /*下方导航栏*/
  #nav-bottom {
    height: 210px;
    background-color: rgb(229,232,233);
    padding-top: 20px;
    position: relative;
  }
  #nav-bottom>h3 {
    width: 400px;
    margin: auto;
    text-align: center;
  }
  #nav-bottom>span {
    font-size: 22px;
    font-weight: bold;
    color: rgb(90,109,116);
    position: absolute;
    top: 20px;
    right: 30px;
    cursor: pointer;
  }
  #nav-bottom>p {
    width: 280px;
    margin: auto;
    text-align: center;
    margin-top: 20px;
    color: rgb(90,109,116);
  }
  #nav-bottom>button {
    width: 180px;
    height: 45px;
    color: white;
    font-size: 18px;
    background-color: rgb(0,218,224);
    outline: none;
    border: none;
    border-radius: 4px;
    position: absolute;
    left: 50%;
    margin-left: -90px;
    margin-top: 20px;
    cursor: pointer;
  }

  /*蒙版*/
  #mask {
    width: 100%;
    height: 100%;
    background-color: black;
    opacity: 0.8;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 30;
  }
  /*下载APP*/
  #app {
    width: 570px;
    height: 570px;
    position: fixed;
    left: 50%;
    margin-left: -235px;
    z-index: 80;
  }
  /*登录*/
 .lore {
    position: absolute;
    z-index: 77;
    color: white;
    width: 540px;
    background-color: white;
    top: 100px;
    left: 50%;
    margin-left: -270px;
  }
  .lore>p>img {
    vertical-align: middle;
    margin-left: 200px;
    margin-right: 10px;
  }
  .lore>p>span {
    font-size: 18px;
    font-weight: bold;
    position: absolute;
    top: 23px;
  }
  .lore>p {
    background-color: black;
    padding: 20px 0;
    position: relative;
  }

  /*微博微信*/
 .sina {
    margin-top: 40px;
    text-align: center;
  }
  .sina>p {
    color: rgb(166,167,167);
    font-size: 14px;
    margin-top: 20px;
  }
  .sina>a>img {
    width: 30px;
  }
  .sina>a:nth-child(1) {
    margin-right: 25px;
  }
  .line {
    width: 140px;
    height: 1px;
    display: inline-block;
    margin-right: 25px;
    margin-left: 25px;
    background-color: rgb(215,216,216);
  }
  .or {
    position: absolute;
    display: inline-block;
    color: rgb(215,216,216);
    font-size: 14px;
    left: 255px;
    top: 207px;
  }
  .ipt {
    width: 400px;
    height: 40px;
    margin-left: 70px;
    margin-top: 25px;
    outline: none;
    border: none;
    background-color: rgb(247,247,247);
    padding-left: 15px;
  }
  /*验证码*/
  .yanzhengma {
    display: inline-block;
    padding: 7px 15px;
    color: white;
    font-weight: bold;
    background-color: rgb(0,218,224);
    border-radius: 4px;
    position: absolute;
    left: 360px;
    top: 313px;
  }
  .noaccount {
    width: 410px;
    overflow: hidden;
    margin: auto;
    margin-top: 20px;
  }
 .noaccount>a:nth-child(1) {
    float: left;
    font-size: 15px;
    text-decoration: none;
    color: rgb(166,167,167);
  }
 .noaccount>a:nth-child(2) {
    float: right;
    padding-left: 20px;
    background: url("../../assets/lock.png") no-repeat ;
    background-size: 20px;
    font-size: 15px;
    text-decoration: none;
    color: rgb(38,45,47);
  }
  .lrbtn {
    width: 400px;
    background-color: rgb(0,218,224);
    margin-left: 70px;
    margin-top: 40px;
    font-size: 18px;
    margin-bottom: 30px;
  }
  /*用户协议*/
  #agreement {
    overflow: hidden;
    width: 420px;
    margin: auto;
    margin-top: 20px;
  }
  #agreement a {
    text-decoration: none;
  }
  #agreement>p {
    float: left;
  }
  #agreement>p>span {
    color: rgb(51,64,63);
    font-size: 12px;
  }
  #agreement>a {
    float: right;
    font-size: 12px;
    display: inline-block;
    margin-top: 4px;
    color: rgb(38,45,47);
  }
  .close {
    position: absolute;
    font-size: 20px;
    font-weight: bold;
    color: rgb(184,185,185);
    top: 5px;
    left: 560px;
    cursor: pointer;
  }
  /*忘记密码*/
  #forgetPassword {
    text-align: center;
    font-size: 18px;
    font-weight: 800;
    margin-bottom: 20px;
  }
  /*验证码*/
 .authCode {
   position: absolute;
   padding: 7px 15px;
   color: white;
   font-weight: bold;
   background-color: rgb(0,218,224);
   border-radius: 4px;
   left: 360px;
   top: 175px;
  }
  #up {
    width: 40px;
    height: 40px;
    background-color: #A3A6A6;
    text-align: center;
    line-height: 40px;
    border-radius: 6px;
    position: fixed;
    right: 20px;
    bottom: 150px;
  }
</style>
