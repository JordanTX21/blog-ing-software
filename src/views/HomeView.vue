<template>
  <div>
    <!-- Page Header-->
    <header class="masthead" style="background-image: url('/img/home-bg.jpg')">
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="site-heading">
              <h1>Blog Grupo 4</h1>
              <span class="subheading">Blog del curso de ingenieria de software</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <div class="container px-4 px-lg-5">
      <div class="row gx-4 gx-lg-5 justify-content-center">
        <div class="col-md-10 col-lg-8 col-xl-7">
          <div v-for="(post,index) in posts" :key="`post-${post.title}`">
            <!-- Post preview-->
            <div class="post-preview">
              <a href="#" class="" @click.prevent="toPost(post,index)">
                <h2 class="post-title">{{post.title}}</h2>
                <h3 class="post-subtitle">Semana {{index+2}}</h3>
              </a>
              <p class="post-meta">
                Publicado por
                <RouterLink to="/" :key="`to-home-${index}`">{{post.by}}</RouterLink>
                el {{post.date}}
              </p>
            </div>
            <!-- Divider-->
            <hr class="my-4" />
          </div>
          <!-- Pager-->
          <div class="d-flex justify-content-end mb-4"><a class="btn btn-primary text-uppercase" href="#!">Otros Posts
              →</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script >
import { usePostStore } from '@/stores/counter'
import posts from '@/data'

export default {
  data() {
    return {
      store: usePostStore(),
      posts: posts
    }
  },
  methods: {
    toPost(post,index) {
      this.store.title = post.title
      this.store.paragraphs = post.paragraphs
      this.store.references = post.references
      this.store.by = post.by
      this.store.date = post.date
      //, params: { title: post.title, paragraphs: post.paragraphs, references: post.references } 
      this.$router.push({ name: 'semana', params: {semana: index} })
    }
  }
}
</script>