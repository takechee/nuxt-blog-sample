<template>
  <section class="main-content">
    <div class="container">
      <h1 class="title has-text-centered">Recent Posts.</h1>
      <div class="columns is-multiline">
        <div class="column is-half" v-for="(post, index) in posts" :key="index">
          <div class="card">
            <header class="card-header">
              <p class="card-header-title">
                {{ post.fields.title }}
              </p>
            </header>
            <div class="card-content">
              <div class="content">
                {{ post.fields.summary }}
                <br />
                <small>
                  by <strong>{{ post.fields.author }}</strong> \\ {{ post.fields.published }}
                </small>
                <img :src="post.fields.thumbnail.fields.file.url"/>
              </div>
            </div>
            <footer class="card-footer">
              <nuxt-link :to="`/post/${post.sys.id}`" class="card-footer-item">
                Read More
              </nuxt-link>
            </footer>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>

export default {
  props: {
    posts: {
      type: Array,
      default: () => {
        return [];
      }
    },
  },
}
</script>
