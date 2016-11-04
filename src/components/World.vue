<template>
  <div class="world">
    <div>
        <span class="bg-primary">{{msg}}</span><br>
        <button class="ui button" @click="getdata">数据载入</button>
        <br><br>
        <hr>
    </div>
    <div class="content1">
        <ul>
            <li v-for="item in articles" >
                <div class="ui card">
                  <div class="content">
                    <span class="right floated meta">14h</span>
                    <span class="left floated meta">
                        <img class="ui avatar image" src="../../static/logo.png"> Elliot
                    </span>
                  </div>
                  <div class="image setheight">
                    <img :src="item.coverUrl">
                  </div>
                  <div class="content">
                    <span class="right floated">
                      <i class="heart outline like icon"></i>
                      17 likes
                    </span>
                    <span class="left floated">
                      <i class="comment icon"></i>
                      3 comments
                    </span>
                  </div>
                  <div class="extra content left">
      
                    <div class="ui large">
                      <i class="heart outline icon"></i>
                      {{ item.title }}
                    </div>
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
//import alert from 'vue-strap/src/Alert.vue'


export default {
  name: 'world',
  components: {
      alert
  },
  data () {
    return {
      msg: '这是semantic-ui样式的demo',
      articles: [
        {
          title:"这是文章标题列表",
          year:2016,
          images:{large:"../static/logo.png"},
          alt:"http://www.douban.com",
          coverUrl:"../static/logo.png"
        }
      ],
      loading:"这是vue-strap样式的demo"
    }
  },
  methods: {
    getdata: function (e) {
      var that = this
      that.loading = '数据加载中...'
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
        },
        error(err) {
          console.log(err)
        }
      })
    },
    click: function(){
      console.log('点击按钮事件触发...')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.content1{
  margin:0 auto;
  width:500px;
  background:#fdfdfd;
}
ul {
  list-style-type: none;
  padding: 0;
  text-align: center;
}

li{
  padding-top:15px;
}

a {
  color: white;
  text-decoration:none; 
}
.span2{
  margin:0 auto;
  display:block;
  width:96%;
  height:80px;
  text-align:left;
  background:white;
  color:gray;
}
.setheight{
    height: 290px;
}
.title{
  padding:10px;
  text-align:left;
}
.divid{
  padding:0;
}
.postfrom{
  color:#999;
  font-size:12px;
  text-align:left;
  padding:10px;
  width:220px;
}
.line{
  margin:0;
  padding:0;
  border-bottom:1px solid #ededed;
  width:100%;
}
.card{
  margin: 30px;
  width:440px;
  border-top-left-radius:10px;
  border-top-right-radius:10px;
}
a{
  color:#555;
}
.alert-icon-float-left {
  font-size:32px;
  float:left;
  margin-right:5px;
}
.left{
  text-align:left;
}
</style>
