<template>
  <div>
    <div class="container">
      <div class="post">
        <h2>{{ post.title.rendered }}</h2>
        <div v-html="post.content.rendered" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  async asyncData({ params, payload }) {
    if (payload) {
      return {
        post: payload,
      }
    } else {
      return await axios
        .get(`http://nuxtwordpress.local/wp-json/wp/v2/posts/${params.id}`)
        .then((res) => {
          return {
            post: res.data,
          }
        })
    }
  },
  data() {
    return {
      post: {},
    }
  },
}
</script>
