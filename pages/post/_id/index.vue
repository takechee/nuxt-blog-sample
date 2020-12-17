<template>
  <div class="main-content">
    <div class="container">
      <h2 class="title is-2">{{ post.title }}</h2>
      <div v-html="toHtmlString(post.content)"></div>
      <br />
      <h4 class="title is-5 is-marginless">
        by <strong>{{ post.author }}</strong> at
        <strong>{{ post.published }}</strong>
      </h4>
    </div>
  </div>
</template>
<script>
// import posts saved JSON data
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import { createClient } from '~/plugins/contentful.js'

const client = createClient()

export default {
  asyncData({ params }, callback) {
    client
      .getEntry(params.id)
      .then((post) => {
        callback(null, { post: post.fields })
      })
      .catch(() => {
        callback({ statusCode: 404, message: 'Post not found' })
      })
  },
  head() {
    return {
      title: this.post.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.post.summary,
        },
      ],
    }
  },
  methods: {
    toHtmlString(obj) {
      return documentToHtmlString(obj)
    },
  },
}
</script>
