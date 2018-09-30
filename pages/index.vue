<template>
  <div>
    <h1>記事一覧</h1>
    <ul>
      <li v-for="post in posts" v-bind:key="post.fields.slug">
        <nuxt-link :to="{ name: 'posts-slug', params: { slug: post.fields.slug, id: post.sys.id }}">
          {{ post.fields.title }}
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
  import {createClient} from '~/plugins/contentful.js'

  const client = createClient()

  export default {
    asyncData ({env}) {
      return Promise.all([
        client.getEntries({
          'content_type': env.CTF_BLOG_POST_TYPE_ID,
          order: '-sys.createdAt'
        })
      ]).then(([posts]) => {
        return {
          posts: posts.items
        }
      }).catch(console.error)
    }
  }
</script>
