<template>
  <div>
    <SearchBar />
    <h1>Blog</h1>
    <div class="grid grid-cols-2 gap-4 mb-10">
      <div
        v-for="post in posts"
        :key="post.id"
        class="bg-white rounded-lg shadow overflow-hidden"
      >
        <NuxtLink :to="`/blog/${post.slug}`">
          <img
            :src="post.image"
            :alt="post.title"
            class="w-full h-48 object-cover"
          />
        </NuxtLink>
        <div class="prose prose-a:no-underline pt-4 p-2">
          <h2>
            <NuxtLink :to="`/blog/${post.slug}`">{{ post.title }}</NuxtLink>
          </h2>
          <p class="line-clamp-3">{{ post.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { wisp } from "~/plugins/wispClient";

const posts = ref([]);

onMounted(async () => {
  const response = await wisp.getPosts({ limit: "all" });
  posts.value = response.posts;
});
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
