<template>
  <div>
    <div id="title">
        <div id="content">
          <div>
            <img src="../../assets/big.png" alt="">
            <span>搜索:&nbsp;&nbsp;{{url}}</span>
            <ul id="list">
              <li v-for="(v,i) in listArray">
                <div class="ball" :style="{backgroundColor:'darkgray'}" v-if="!v.isTopic"></div>
                <div class="ball" :style="{backgroundColor:'#00DAE0'}" v-if="v.isTopic"></div>
                <a href="#" class="location">
                  {{v.content}}
                </a>
              </li>
            </ul>
          </div>
        </div>
    </div>
    <h4>相关深度阅读</h4>
    <div id="related">
      <div v-for="(v,i) in aboutArray" class="box">
        <img :src="v.banner" alt="">
        <div class="mask"></div>
        <div class="title">
          <a href="#">
            {{v.title}}
          </a>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    var url = window.location.href.split('?')[1]
    var name = ''
    if (url != undefined) {
      name = url.split('=')[1]
    }
    export default {
        name: '',
        data() {
          return {
            name:name,
            url:'',
            listArray:[],
            aboutArray:[]
          }

        },
        mounted (){
          var _that = this
          axios.get('api/search?q='+this.name).then(
            function (res) {
              _that.url = res.data.query.q
              _that.listArray = res.data.query.tags
            }
          )
          axios.get('api/search/articles?q='+this.name).then(
            function (res) {
              console.log(res.data)
              _that.aboutArray = res.data.pgcs
            }
          )
        }
    }
</script>

<style scoped>
  #title {
    height: 120px;
    background-color: white;
    padding: 20px;
  }
  #content {
    width: 980px;
    margin: auto;
  }
  #content>div>img {
    vertical-align: middle;
  }
  /*球*/
  .ball {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    display: inline-block;
    margin-right: 10px;
  }
ul {
  margin-top: 15px;
}
 #list>li {
   list-style: none;
   display: inline-block;
   margin-right: 15px;
 }
  #list>li:nth-child(1) {
    margin-left: -35px;
  }
  .location {
    text-decoration: none;
    color: #A6A8AA;
    font-size: 14px;
  }
  h4 {
    width: 300px;
    text-align: center;
    margin: auto;
    margin-top: 30px;
  }
  #related {
    width: 960px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    border: 1px solid red;
    margin: auto;
    margin-top: 20px;
  }
  .box {
    width: 218px;
    height: 180px;
    position: relative;
    overflow: hidden;
    border-radius: 4px;
  }
  .mask {
    position: absolute;
    width: 218px;
    height: 180px;
    left: 0;
    top: 0;
    background-color: rgba(0,0,0,0.2);
  }
  .title {
    position: absolute;
    top: 30%;
    width: 170px;
    left: 50%;
    margin-left: -85px;
  }
  .title>a {
    text-decoration: none;
    color: white;
    font-weight: 500;
  }
</style>
