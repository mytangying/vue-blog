<template>
  <div id="fh5co-main">
    <div class="fh5co-narrow-content animate-box" data-animate-effect="fadeInLeft">
      <div class="row">
        <div class="col-md-4">
          <h2 class="fh5co-heading">Get In Touch</h2>
        </div>
      </div>
      <form action="">
        <div class="row">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-6">
                <div class="form-group">
                  <input type="text" class="form-control" placeholder="Name">
                </div>
                <div class="form-group">
                  <input type="text" class="form-control" placeholder="Email">
                </div>
                <div class="form-group">
                  <input type="text" class="form-control" placeholder="Phone">
                </div>
              </div>
              <div class="col-md-6">
                <div class="form-group">
                  <textarea name="" id="message" cols="30" rows="7" class="form-control" placeholder="Message"></textarea>
                </div>
                <div class="form-group">
                  <input type="submit" class="btn btn-primary btn-md" value="Send Message">
                </div>
              </div>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      msg: '登录'
    }
  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
