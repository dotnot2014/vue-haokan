<template>
  <div class="hello">
    <div>
        <span>{{msg}}</span><br>
        <x-button mini  @click="getdata" type="default" >数据载入</x-button>
        <br>
        <divider>{{loading}}</divider>
    </div>
    <div class="content">
        <ul>
            <li v-for="item in articles" >
                <div class="card">
                  <img  :src="item.coverUrl" class="img">
                  <div  class="span2">
                    <p class="title">
                      <a :href="item.articleUrl">
                        {{ item.title }}
                      </a>
                    </p>
                    <p class="line"></p>
                    <p class="postfrom">
                      <span >2016-11-2</span>&nbsp;&nbsp;&nbsp;
                      <span >From ：花儿好看</span>
                    </p>
                  </div>
                </div>
            </li>
        </ul>
    </div>
  </div>
</template>


<script>
import reqwest from "reqwest"
import group from 'vux/src/components/group'
import divider from 'vux/src/components/divider'
import Xbutton from 'vux/src/components/x-button'
//import card from 'vux/src/components/card'


export default {
  name: 'hello',
  components: {
    divider,
    group,
    'x-button':Xbutton,
    //card
  },
  data () {
    return {
      msg: '推荐图文-花儿好看',
      articles: [
        {
          title:"这是文章标题列表",
          year:2016,
          images:{large:"../static/logo.png"},
          alt:"http://www.douban.com",
          coverUrl:"../static/logo.png"
        }
      ],
      loading:"华丽丽的分割线"
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
@import '~vux/dist/vux.css';

.content{
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
.img{
  display:block;
  width:96%;
  height:270px;
  margin-top: 10px;
  margin-left: 10px;
  border-top-left-radius:10px;
  border-top-right-radius:10px;
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
  margin: 10px;
  border-top-left-radius:10px;
  border-top-right-radius:10px;
}
a{
  color:#555;
}
</style>
