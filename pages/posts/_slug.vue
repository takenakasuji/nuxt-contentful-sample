<template>
  <div>{{ entry }}</div>
</template>

<script>
import {createClient} from '~/plugins/contentful.js'

const client = createClient()

export default {
  asyncData ({ env, params }) {
    console.log(params)
    // return client.getEntries({
    //     'content_type': env.CTF_BLOG_POST_TYPE_ID,
    //     order: '-fields.publishDate'
    //   }).then(entries => {
    //     const posts = entries.items
    //     const current = posts.filter(function (item) {
    //       return item.fields.slug === params.slug
    //     })
    //     return {
    //       allPosts: posts,
    //       currentPost: current[0]
    //     }
    //   }).catch(console.error)
    return client.getEntry(params.id)
    .then( entry => {
      return {
        entry: entry
      }
    })
    .catch(console.error)
  }
}
</script>
