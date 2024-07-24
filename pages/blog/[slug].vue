<template>
  <div>
    <div class="mb-4">
      <NuxtLink :to="`/`">Back</NuxtLink>
    </div>
    <div v-if="post" class="prose">
      <h1>{{ post.title }}</h1>
      <div v-html="post.content"></div>
      <div v-if="post.tags && post.tags.length" class="tags">
        <div v-if="post.tags && post.tags.length" class="tags mt-4">
          <div
            v-for="tag in post.tags"
            :key="tag.id"
            class="inline-block bg-slate-200 py-2 px-4 rounded-full mr-2 mt-2"
          >
            <NuxtLink :to="`/tags/${tag.name}`">#{{ tag.name }}</NuxtLink>
          </div>
        </div>
      </div>
      <h2>Related Posts</h2>
      <ul>
        <li
          v-for="relatedPost in relatedPosts"
          :key="relatedPost.id"
          class="list-disc list-inside"
        >
          <NuxtLink :to="`/blog/${relatedPost.slug}`">{{
            relatedPost.title
          }}</NuxtLink>
        </li>
      </ul>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import { wisp } from "~/plugins/wispClient";

const route = useRoute();
const post = ref(null);
const relatedPosts = ref([]);

onMounted(async () => {
  const response = await wisp.getPost(route.params.slug);
  post.value = response.post;
  const relatedResponse = await wisp.getRelatedPosts({
    slug: route.params.slug,
    limit: 5,
  });
  relatedPosts.value = relatedResponse.posts;
});
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
