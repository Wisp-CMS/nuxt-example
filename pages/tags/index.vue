<template>
  <div>
    <h1>Tags</h1>
    <ul>
      <li v-for="tag in tags" :key="tag.id">
        <NuxtLink :to="`/tags/${tag.name}`">{{ tag.name }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { wisp } from '~/plugins/wispClient'

const tags = ref([])

onMounted(async () => {
  const response = await wisp.getTags()
  tags.value = response.tags
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