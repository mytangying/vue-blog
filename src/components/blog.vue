<template>
  <div id="fh5co-main">
    <div class="fh5co-narrow-content">
      <h2 class="fh5co-heading animate-box col-sm-6" data-animate-effect="fadeInLeft">阅读我的博客</h2>
      <div class="form-group  animate-box col-sm-6" data-animate-effect="fadeInLeft">
        <input type="search" class="form-control" placeholder="搜索" v-model="searchmess" @keyup="search">
        <img src="../../static/images/search.png" class="search-btn" @click="search">
      </div>
      <div class="row row-bottom-padded-md">
        <div class="col-md-3 col-sm-6 col-padding animate-box " data-animate-effect="fadeInLeft" v-for="item in data ">
          <router-link :to="'/content?id='+item.id" class="blog-entry blog-box">
            <div class="blog-img"><img :src="'../../static/images/'+item.id+'.jpg'" class="img-responsive"></div>
            <div class="desc">
              <h3>{{item.title}}</h3>
              <span><small>日期</small>：<small>{{item.pub_date | timefil}}</small></span>
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
              <a class="btn btn-primary" @click="more">点击加载更多博客</a>
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
  Vue.filter('timefil', function (value) {
    if (!value) {
      return ''
    }
    value = value.toString()
    return value.slice(0, 19).replace('T', ' ')
  })

  export default {
    data() {
      return {
        data: '',
        domain: 'http://www.wangyanan.win:8000/',
        searchmess: '',
        dbdata: '',
        param: '1'
      }
    },
    mounted() {
      // GET /someUrl
      this.$http.get(this.domain + 'blog/pagination/' + this.param + '/8').then(response => {
        this.data = response.data
        this.dbdata = response.data
      }, response => {
        console.log('error')
      })
    },
    methods: {
      search() {
        var res = []
        for (var i = 0; i < this.dbdata.length; i++) {
          if (this.searchmess === '') {
            res = this.dbdata
          } else if (this.dbdata[i].title.indexOf(this.searchmess) !== -1) {
            res.push(this.dbdata[i])
          }
        }
        this.data = res
      },
      more() {
        this.param++
        this.$http.get(this.domain + 'blog/pagination/' + this.param + '/8').then(response => {
          if (response.data.length > 0) {
            for (var i = 0; i < response.data.length; i++) {
              this.dbdata.push(response.data[i])
            }
          } else {
            alert('已加载全部博客')
            return
          }
          this.data = this.dbdata
        }, response => {
          console.log('error')
        })
      }
    }
  }

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
