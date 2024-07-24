<template>
  <div>
    <input 
      v-model="query" 
      @keyup.enter="onSearch" 
      placeholder="Search..." 
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const query = ref('')
const router = useRouter()

const onSearch = () => {
  if (query.value.trim()) {
    router.push({ path: '/search', query: { q: query.value.trim() } })
  }x
}
</script>

<style scoped>
div {
  margin: 1em 0;
}
input {
  width: 100%;
  padding: 0.5em;
  font-size: 1em;
}
</style>
