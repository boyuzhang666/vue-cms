<template>
  <div class="container">
    <div class="news-head">
      <h4>{{newsinfo.title}}</h4>
      	<p class="mui-ellipsis news-time">
          <span>发表时间:{{newsinfo.add_time | dateformatter("YYYY-MM-DD HH:mm:ss")}}</span>
          <span class="mui-pull-right">点击{{newsinfo.click}}次</span>
        </p>
    </div>
    <div class="news-content" v-html="newsinfo.content"></div>
    <div class="news-comment">
      <comment :id="this.$route.params.id"></comment>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import dateformatter from "../../filters/dateformatter"
import comment from "../common/comment.vue"

export default {
  data(){
    return {
      newsinfo:{}
      // id:1
    }
  },
  created(){
    axios({
      url:"http://vue.studyit.io/api/getnew/" + this.$route.params.id
    }).then(res => {
      if(res.data.message.length > 0){
        console.log(res.data.message);
        this.newsinfo = res.data.message[0];
      }
    })
  },
  components:{
    comment
  },
  filters:{
    dateformatter
  }
};
</script>

<style>
  .news-head,.news-content,.news-comment{
    padding: 5px;
  }
  .news-content img{
    width: 100%;
  }
  .news-time{
    font-size: 12px;
  }
</style>
