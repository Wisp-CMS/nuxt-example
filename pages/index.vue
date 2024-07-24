<template>
  <div>
    <SearchBar />
    <h1>Blog</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">
        <NuxtLink :to="`/blog/${post.slug}`">{{ post.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { wisp } from '~/plugins/wispClient'

const posts = ref([])

onMounted(async () => {
  const response = await wisp.getPosts({ limit: 'all' })
  posts.value = response.posts
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
</style>