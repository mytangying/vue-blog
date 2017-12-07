<template>
  <div id="fh5co-main">
    <div class="fh5co-narrow-content">
      <h2 class="fh5co-heading animate-box" data-animate-effect="fadeInLeft">{{data.title}}</h2>
      <h5 class="fh5co-label animate-box" data-animate-effect="fadeInLeft">标签：<span v-for="val in data.labels">{{val}}&nbsp;&nbsp;&nbsp;</span>
      </h5>
      <div class="row row-bottom-padded-md">
        <div class="col-sm-12 col-padding animate-box" data-animate-effect="fadeInLeft">
          <div class="blog-entry" v-hljs v-html="data.html">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Vue from 'vue'
import VueResource from 'vue-resource'
import HyperDown from '../../static/js/Parser'
import hljs from '../../static/js/highlight.js'

Vue.directive('hljs', el => {
  let blocks = el.querySelectorAll('pre code')
  Array.prototype.forEach.call(blocks, hljs.highlightBlock)
})

Vue.use(VueResource)
Vue.filter('timefil', function(value) {
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
      id: window.location.hash.slice(13),
      domain: 'http://www.wangyanan.win:8000/',
      doc: ''
    }
  },
  mounted: function() {
    // GET /someUrl
    this.$http.get(this.domain + 'blog/article/' + this.id + '/').then(response => {
      this.data = response.data
      var parser = new HyperDown()
      this.data.html = (response.data.richText !== 'richText' && response.data.richText !== '') ? response.data.richText : parser.makeHtml(this.data.content)
    }, response => {
      console.log('error')
    })
  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.blog-entry {
  padding: 3% 7% 5%;
}

@media (min-width:768px) {
  .blog-entry {
    padding: 3% 4% 5%;
  }
}

#fh5co-main {
  font-family: "Vollkorn", Palatino, Times;
}

@import "../../static/css/foghorn.css";
@import "../../static/css/monokai-sublime.css";

</style>
