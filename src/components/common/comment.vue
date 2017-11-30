<template>
  <div class="container">
    <h4>发表评论</h4>
    <textarea v-model="cmtInfo" name="" id="" cols="30" rows="10"></textarea>
    <mt-button type="primary" size="large" @click="postCmt">发表评论</mt-button>
    <ul class="mui-table-view">
				<li class="mui-table-view-cell mui-media" v-for="(item,index) in commentList" :key="index">
					<a href="javascript:;">
            <p class="mui-ellipsis news-time">
              <span>发表时间:{{item.add_time | dateformatter("YYYY-MM-DD HH:mm:ss")}}</span>
              <span class="mui-pull-right">{{item.user_name}}</span>
            </p>
						<img class="mui-media-object mui-pull-right" :src="'../../images/menu'+ Math.ceil(Math.random()*6) +'.png'">
						<div class="mui-media-body">
							{{item.title}}
							<p class="mui-ellipsis">{{item.content}}</p>
						</div>
					</a>
				</li>
			</ul>
      <mt-button type="danger" v-if="isShowLoadMore" plain size="large" @click="loadMore">加载更多</mt-button>

  </div>
</template>

<script>
import axios from "axios";
import dateformatter from "../../filters/dateformatter.js";

import { Toast } from "mint-ui";

export default {
  data() {
    return {
      commentList: [],
      cmtInfo: "",
      isShowLoadMore: true,
      pageindex: 1
    };
  },
  created() {
    this.getData();
  },
  methods: {
    getData() {
      axios({
        url:
          "http://vue.studyit.io/api/getcomments/" +
          this.id +
          "?pageindex=" +
          this.pageindex
      }).then(res => {
        if (res.data.message.length > 0) {
          this.commentList = this.commentList.concat(res.data.message);
        } else {
          Toast("没有更多数据了");
          this.isShowLoadMore = false;
        }
      });
    },
    postCmt() {
      Toast(this.cmtInfo);
      if (this.cmtInfo.trim()) {
        axios({
          url: "http://vue.studyit.io/api/postcomment/" + this.id,
          method: "post",
          data: "content=" + this.cmtInfo
        }).then(res => {
          if (res.data.status == 0) {
            this.commentList.unshift({
              user_name: "匿名用户",
              add_time: new Date(),
              content: this.cmtInfo
            });
            this.cmtInfo = "";
          }
        });
      }
    },
    loadMore() {
      this.pageindex++;
      this.getData();
    }
  },
  filters: {
    dateformatter
  },
  props: ["id"]
};
</script>

<style scoped>
textarea {
  height: 150px;
}
</style>
