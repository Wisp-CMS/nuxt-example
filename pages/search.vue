<template>
  <div>
    <h1>Search Results</h1>
    <ul v-if="posts.length">
      <li v-for="post in posts" :key="post.id">
        <NuxtLink :to="`/blog/${post.slug}`">{{ post.title }}</NuxtLink>
      </li>
    </ul>
    <p v-else>No results found.</p>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'
import { wisp } from '~/plugins/wispClient'

const route = useRoute()
const posts = ref([])

const searchPosts = async (query) => {
  const response = await wisp.getPosts({ query })
  posts.value = response.posts
}

onMounted(() => {
  searchPosts(route.query.q)
})

watch(() => route.query.q, (newQuery) => {
  searchPosts(newQuery)
})
</script>

<style scoped>
h1 {
  font-size: 2em;
  margin-bottom: 0.5em;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  margin-bottom: 0.5em;
}
p {
  font-size: 1em;
  font-style: italic;
}
</style>