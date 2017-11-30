<template>
  <div>
    <mt-header fixed title="固定在顶部">
        <router-link to="/" slot="left">
          <mt-button icon="back">返回</mt-button>
        </router-link>
    </mt-header>

    <router-view>
		</router-view>

    <nav class="mui-bar mui-bar-tab">
			<a class="mui-tab-item mui-active" href="#tabbar">
				<span class="mui-icon mui-icon-home"></span>
				<span class="mui-tab-label">首页</span>
			</a>
			<a class="mui-tab-item" href="#tabbar-with-chat">
				<span class="mui-icon mui-icon-contact"></span>
				<span class="mui-tab-label">会员</span>
			</a>
			<a class="mui-tab-item" href="#tabbar-with-contact">
				<span class="mui-icon mui-icon-contact"><span class="mui-badge">9</span></span>
				<span class="mui-tab-label">购物车</span>
			</a>
			<a class="mui-tab-item" href="#tabbar-with-map">
				<span class="mui-icon mui-icon-search"></span>
				<span class="mui-tab-label">搜索</span>
			</a>
		</nav>


  </div>
  
</template>

<script>
export default {};
</script>

<style>
html,body{
	height: 100%;
	background-color: #fff;
}
.container {
  margin-top: 40px;
	margin-bottom: 50px;
}
</style>
