<template>
  <div class="container mx-auto px-4">
    <h2 class="text-lg font-bold">記事の更新確認</h2>
    <div v-for="(post, index) in posts" :key="index" class="grid grid-cols-3">
      <div>
        <nuxt-link :to="`/blog/${post.id}`">
          {{ post.title }}
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, error }) {
    try {
      const entries = await $axios.get(
        `${$config.apiUrl}${$config.siteId}/entries`
      )
      return {
        posts: entries.data.items,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>

<style></style>
