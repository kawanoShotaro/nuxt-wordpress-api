<template>
  <div>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('img/post-bg.jpg')" v-if="post">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{post.title}}</h1>
              <span class="meta">Posted by
              <a href="#">{{post.author.name}}</a>
              on {{date}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article v-if="post">
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="post.content"/>
        </div>
      </div>
    </article>
  </div>
</template>

<script>
  import dayjs from "dayjs"

  export default {
    data(){
      return {
        post: null
      }
    },
    computed: {
      id(){
        return this.$route.params.id
      },
      date(){
        const date = new Date(this.post.date)
        return dayjs(this.post.date).format("MMMM-DD, YYYY")
      }
    },
    async mounted() {
      const {data} = await this.$axios.get(`sites/nuxtjsblog.wordpress.com/posts/${this.id}`)
      this.post = data
    }
  }
</script>

<style>
</style>