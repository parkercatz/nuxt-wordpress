<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">nuxt-wordpress</h1>
      <div class="posts">
        <h2>記事一覧</h2>
        <div v-for="post in posts" :key="post.id" class="post">
          <h3>{{ post.title.rendered }}</h3>
          <div class="post-content" v-html="post.excerpt.rendered" />
          <nuxt-link
            :to="{
              name: 'slug',
              params: { slug: post.slug, id: post.id },
            }"
          >
            Read More
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  fetch({ store }) {
    return axios
      .get('http://nuxtwordpress.local/wp-json/wp/v2/posts')
      .then((res) => {
        store.commit('frontPagePosts', res.data)
      })
      .catch((err) => {
        console.log(err)
      })
  },
  computed: {
    posts() {
      return this.$store.state.posts
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
