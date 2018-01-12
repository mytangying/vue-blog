<template>
  <div id="fh5co-main">
    <aside id="fh5co-hero" class="js-fullheight">
      <div class="flexslider js-fullheight">
        <ul class="slides">
          <li style="background-image: url(../../static/images/img_bg_1.jpg);">
            <div class="overlay"></div>
            <div class="container-fluid">
              <div class="row">
                <div class="col-sm-12 text-center js-fullheight slider-text">
                  <div class="slider-text-inner">
                    <h1>你好<strong></strong>,欢迎来到树甙芎的博客</h1>
                  </div>
                </div>
              </div>
            </div>
          </li>
          <li style="background-image: url(../../static/images/img_bg_2.jpg);">
            <div class="overlay"></div>
            <div class="container-fluid">
              <div class="row">
                <div class="col-sm-12 text-center js-fullheight slider-text">
                  <div class="slider-text-inner">
                    <h1>移动端点击左上角查看导航栏</h1>
                  </div>
                </div>
              </div>
            </div>
          </li>
          <li style="background-image: url(../../static/images/img_bg_3.jpg);">
            <div class="overlay"></div>
            <div class="container-fluid">
              <div class="row">
                <div class="col-sm-12 text-center js-fullheight slider-text">
                  <div class="slider-text-inner">
                    <h1>向下滑动开始 Let's Go</h1>
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
        <div class="start">
          <p>开始</p>
          <img src="../../static/images/arrow.png">
        </div>
      </div>
    </aside>
    <div class="fh5co-narrow-content">
      <h2 class="fh5co-heading animate-box" data-animate-effect="fadeInLeft">近期博客</h2>
      <div class="row row-bottom-padded-md">
        <div class="col-md-3 col-sm-6 col-padding animate-box" data-animate-effect="fadeInLeft" v-for="item in data">
          <router-link :to="'/content?id='+item.id" class="blog-entry">
            <div class="blog-img"><img :src="'../../static/images/'+item.id+'.jpg'" class="img-responsive"></div>
            <div class="desc">
              <h3>{{item.title}}</h3>
              <span><small>日期</small>：<small>{{item.pub_date|timefil}}</small></span>
              <span><small>标签</small>：<small v-for="val in item.labels">{{val}}&nbsp;&nbsp;</small></span>
              <span><small>作者</small>：<small>{{item.creator}}&nbsp;&nbsp;</small></span>
              <div class="lead">阅读全文<i class="icon-arrow-right3"></i></div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
    <div id="get-in-touch">
      <div class="fh5co-narrow-content">
        <div class="row">
          <div class="col-md-6 col-md-offset-3 col-md-pull-3 animate-box" data-animate-effect="fadeInLeft">
            <p class="more-blog">
              <router-link to="/blog" class="btn btn-primary">查看更多博客</router-link>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Vue from 'vue'
import VueResource from 'vue-resource'
Vue.use(VueResource)
Vue.filter('timefil', function(value) {
  if (!value) { return '' }
  value = value.toString()

  return value.slice(0, 19).replace('T', ' ')
})
export default {
  data() {
    return {
      data: '',
      domain: 'http://www.wangyanan.win:8000/'
    }
  },
  mounted: function() {
    // GET /someUrl
    this.$http.get(this.domain + 'blog/list/').then(response => {
      this.data = response.data.slice(0, 4)
    }, response => {
      console.log('error')
    })
  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
