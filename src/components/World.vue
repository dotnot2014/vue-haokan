<template>
  <div class="world">
    <div>
      <span class="bg-primary"><i class="china flag"> </i> {{msg}}</span>
      <br>
      <div class="ui icon input">
        <i class="search icon"></i>
        <input v-model="searchtxt" type="text" placeholder="Search..." @keyup.enter="click">
      </div>
      <br><br>
      <div class="ui horizontal divider">组件区</div>
      <div class="ui {{stat}} animated button" tabindex="0" @click="getdata">
        <div class="visible content">数据载入</div>
        <div class="hidden content">
          <i class="right play icon"></i>
        </div>
      </div>
      <br><br>
      <div class="ui info message setwidth">Well done! You successfully read this important alert message.</div>
      <br>
      <div class="ui center aligned basic segment">
        <div class="ui horizontal list left">
          <div class="item">
            <img class="ui mini circular image" src="../../static/molly.png">
            <div class="content ">
              <div class="ui sub header ">Molly</div>Coordinator </div>
          </div>
          <div class="item">
            <img class="ui mini circular image" src="../../static/molly.png">
            <div class="content">
              <div class="ui sub header">Elyse</div>Developer </div>
          </div>
          <div class="item">
            <img src="../../static/molly.png" class="ui mini circular image">
            <div class="content">
              <div class="ui sub header">Eve</div>Project Manager </div>
          </div>
        </div>
        <div class="ui horizontal divider">{{loading}}</div>
      </div>
      <div class="content1">
        <ul>
          <li v-for="item in articles">
            <div class="ui card">
              <div class="content">
                <span class="right floated meta">
                <i class="time icon"></i> {{ item.postTime }}
              </span>
                <span class="left floated meta">
                        <img class="ui avatar image" src="../../static/molly.png"> {{ item.author }}
                    </span>
              </div>
              <div class="image setheight">
                <img :src="item.coverUrl">
              </div>
              <div class="extra content left h-l">
                <div class="ui large">
                  <i class="wechat icon"></i>
                  <a class="astyle" href="{{ item.articleUrl }}">{{ item.title }}</a>
                </div>
              </div>
              <div class="extra content h-s">
                <span class="right floated">
                      <i class="heart outline like icon"></i>
                      17 likes
                </span>
                <span class="left floated">
                      <i class="comment icon"></i>
                      6 comments
                </span>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
</template>
<script>
import reqwest from "reqwest"
import { alert } from 'vue-strap'

export default {
  name: 'world',
  components: {
      alert
  },
  data () {
    return {
      msg: '这是semantic-ui样式的demo',
      tags:[],
      searchtxt:'',
      stat:'',
      articles: [
        {
          title:"这是文章标题列表",
          year:2016,
          images:{large:"../static/logo.png"},
          alt:"http://www.douban.com",
          coverUrl:"../static/logo.png"
        }
      ],
      loading:"数据展示区"
    }
  },
  methods: {
    getdata: function (e) {
      var that = this
      that.loading = '数据加载中...'
      that.stat = 'loading'
      setTimeout(function () {that.fetch()}, 1300)
    },
    click: function(e){
      var that = this
      //that.tags = that.tags.concat(e.target.value)
      that.searchtxt = ''
      console.log(e.target.value)
    },
    fetch: function(){
      var that = this
      reqwest({
        //url: "https://cnodejs.org/api/v1/topics",
        //url:"http://api.douban.com/v2/movie/top250",
        url:"https://hacknews.wilddogio.com/rows.json",
        method: "get",
        type: 'jsonp',
        data: {},
        success(res) {
          that.articles = res
          console.log(res)
          console.log("数据加载完毕...")
          that.loading = '华丽丽的分割线'
          that.stat = ''
        },
        error(err) {
          console.log(err)
        }
      })
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @media (max-width: 767px) {
    .hidden-xs {
      display: none !important;
    }
  }
  
  @media (min-width: 768px) and (max-width: 991px) {
    .hidden-sm {
      display: none !important;
    }
  }
  
  @media (min-width: 992px) and (max-width: 1199px) {
    .hidden-md {
      display: none !important;
    }
  }
  
  @media (min-width: 1200px) {
    .hidden-lg {
      display: none !important;
    }
  }
  
  .content1 {
    margin: 0 auto;
    width: 500px;
    background: #fdfdfd;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
    text-align: center;
  }
  
  li {
    padding-top: 15px;
  }
  
  .ui.card>.extra a:not(.ui):hover {
    color: #333;
  }
  
  .ui.card>.extra a {
    color: #666;
  }
  
  .span2 {
    margin: 0 auto;
    display: block;
    width: 96%;
    height: 80px;
    text-align: left;
    background: white;
    color: gray;
  }
  
  .setheight {
    height: 290px;
  }
  
  .title {
    padding: 10px;
    text-align: left;
  }
  
  .divid {
    padding: 0;
  }
  
  .postfrom {
    color: #999;
    font-size: 12px;
    text-align: left;
    padding: 10px;
    width: 220px;
  }
  
  .line {
    margin: 0;
    padding: 0;
    border-bottom: 1px solid #ededed;
    width: 100%;
  }
  
  .card {
    margin: 30px;
    width: 440px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }
  
  a {
    color: #555;
  }
  
  .alert-icon-float-left {
    font-size: 32px;
    float: left;
    margin-right: 5px;
  }
  
  .left {
    text-align: left;
  }
  
  .ui.card>.image>img {
    display: block;
    width: 100%;
    height: 290px;
    border-radius: inherit;
  }
  
  .h-s {
    height: 30px;
  }
  
  .ui.card>.extra {
    padding: .3em 1em;
  }
  
  .ui.card>.extra.h-l {
    height: 50px;
    padding-top: 1em;
  }
  .setwidth{
    width:450px;
    margin:0 auto;
  }
</style>