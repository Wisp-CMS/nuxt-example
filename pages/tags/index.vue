<template>
  <div>
    <div class="mb-4">
      <NuxtLink :to="`/`">Back</NuxtLink>
    </div>
    <h1>Tags</h1>
    <div>
      <div
        v-for="tag in tags"
        :key="tag.id"
        class="inline-block bg-slate-200 py-2 px-4 rounded-full mr-2 mt-2"
      >
        <NuxtLink :to="`/tags/${tag.name}`">#{{ tag.name }}</NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { wisp } from "~/plugins/wispClient";

const tags = ref([]);

onMounted(async () => {
  const response = await wisp.getTags();
  tags.value = response.tags;
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
