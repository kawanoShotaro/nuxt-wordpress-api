<template>
  <div>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('img/home-bg.jpg')">
      ...
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div v-for="post in posts" :key="post.ID">
            <div class="post-preview">
              <a href="post.html">
                <h2 class="post-title">{{post.title}}</h2>
              </a>
              <p class="post-meta">Posted by
                <a href="#">{{post.author.name}}</a>
                on {{date(post)}}</p>
            </div>
            <hr>
          </div>
          <!-- Pager -->
          <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data(){
    return {
      posts: []
    }
  },
  async mounted() {
    const {data} = await this.$axios.get("sites/xxxxxxxxx.wordpress.com/posts")
    this.posts = data.posts
  },
  methods: {
    date(post){
      const date = new Date(post.date) 
      return dayjs(post.date).format("MMMM-DD, YYYY")
    }
  }
}
</script>

<style>
</style>