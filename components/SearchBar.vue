<template>
  <div >
    <input 
      class="border p-2 rounded-md my-2 w-full focus-visible:outline-gray-600 focus-visible:placeholder:text-gray-600 bg-transparent"
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