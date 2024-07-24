<template>
  <div v-if="post">
    <h1>{{ post.title }}</h1>
    <div v-html="post.content"></div>
    <h2>Related Posts</h2>
    <ul>
      <li v-for="relatedPost in relatedPosts" :key="relatedPost.id">
        <NuxtLink :to="`/blog/${relatedPost.slug}`">{{ relatedPost.title }}</NuxtLink>
      </li>
    </ul>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import { wisp } from '~/plugins/wispClient'

const route = useRoute()
const post = ref(null)
const relatedPosts = ref([])

onMounted(async () => {
  const response = await wisp.getPost(route.params.slug)
  post.value = response.post
  const relatedResponse = await wisp.getRelatedPosts({ slug: route.params.slug, limit: 5 })
  relatedPosts.value = relatedResponse.posts
})
</script>

<style scoped>
h1 {
  font-size: 2em;
  margin-bottom: 0.5em;
}
h2 {
  font-size: 1.5em;
  margin-top: 2em;
}
img {
  max-width: 100%;
  height: auto;
  margin-bottom: 1em;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin-bottom: 0.5em;
}
div {
  font-size: 1em;
  line-height: 1.6;
}
</style>