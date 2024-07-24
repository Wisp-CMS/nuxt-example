<template>
  <div>
    <h1>Posts Tagged: {{ route.params.tag }}</h1>
    <ul>
      <li v-for="post in filteredPosts" :key="post.id">
        <NuxtLink :to="`/blog/${post.slug}`">{{ post.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import { wisp } from '~/plugins/wispClient'

const route = useRoute()
const filteredPosts = ref([])

onMounted(async () => {
  const response = await wisp.getPosts({ tag: route.params.tag })
  filteredPosts.value = response.posts
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