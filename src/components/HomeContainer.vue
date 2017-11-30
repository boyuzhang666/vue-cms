<template>
  <div class="container">
    <div class="swipe">
      <mt-swipe :auto="0">
  			<mt-swipe-item v-for="(item,index) in swipePics" :key="index">
          <img :src="item.img" >
        </mt-swipe-item>
			</mt-swipe>
    </div>

    <ul class="mui-table-view mui-grid-view mui-grid-9">
		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
          <router-link to="/home/newslist">
		          <img src="../images/menu1.png">
		          <div class="mui-media-body">新闻资讯</div>
          </router-link>
        </li>
        		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
		          <img src="../images/menu2.png">
		          <div class="mui-media-body">图片分享</div></a>
        </li>
        		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
		          <img src="../images/menu3.png">
		          <div class="mui-media-body">商品购买</div></a>
        </li>
        		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
		          <img src="../images/menu4.png">
		          <div class="mui-media-body">留言反馈</div></a>
        </li>
        		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
		          <img src="../images/menu5.png">
		          <div class="mui-media-body">视频专区</div></a>
        </li>
        		    <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
		          <img src="../images/menu6.png">
		          <div class="mui-media-body">联系我们</div></a>
        </li>
		</ul>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      swipePics: []
    };
  },
  created() {
    axios({
      url: "http://vue.studyit.io/api/getlunbo"
    }).then(res => {
      if (res.data.message.length > 0) {
        // console.log(res.data.message);
        this.swipePics = res.data.message;
      }
    });
  }
};
</script>

<style>
.swipe {
  height: 220px;
}
.swipe img {
  width: 100%;
}
.mui-table-view .mui-table-view-cell img {
  width: 80%;
}

.mui-grid-view.mui-grid-9 {
  background-color: #fff;
  border: none;
}

.mui-grid-view.mui-grid-9 .mui-table-view-cell {
  border: none;
}
</style>
