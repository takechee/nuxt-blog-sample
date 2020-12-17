<template>
  <div>
    <section class="hero is-medium is-primary is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Welcome to the JavaScript SSR Blog.</h1>
          <h2 class="subtitle">Hope you find something you like.</h2>
        </div>
      </div>
    </section>
    <Posts :posts="posts"/>
  </div>
</template>

<script>
import Posts from '~/components/Posts.vue'
import { createClient } from '~/plugins/contentful.js'

const client = createClient()

export default {
  head: {
    title: 'Home',
  },
  async asyncData({ params }) {
    // 記事一覧を取得
    const entries = await client.getEntries({
      content_type: process.env.CTFL_CONTENT_TYPE_POST
    })
    console.dir(entries.items, { depth: null });
    return {
      posts: entries.items
    }
  },
  components: {
    Posts,
  },
}
</script>

<style></style>
