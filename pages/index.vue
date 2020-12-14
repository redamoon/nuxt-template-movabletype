<template>
  <div class="container mx-auto px-4">
    <h2 class="text-lg font-bold">ブログ記事</h2>
    <div v-for="(post, index) in posts" :key="index" class="grid grid-cols-3">
      <div>
        <a :href="`/blog/${post.id}/`">
          {{ post.title }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, error }) {
    const entries = await $axios.get(
      `${$config.apiUrl}${$config.siteId}/entries`
    )
    return {
      posts: entries.data.items,
    }
  },
}
</script>

<style></style>
