<template>
  <div class="container mx-auto px-4">
    <h2 class="text-lg font-bold">{{ post.title }}</h2>
    <!-- eslint-disable-next-line vue/no-v-html-->
    <div class="body" v-html="post.body"></div>
    <!-- eslint-disable-next-line vue/no-v-html-->
    <div v-html="post.customFields[2].value"></div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config, params, error }) {
    try {
      const { data } = await $axios.get(
        `https://movabletype-knowledge.tech/cgi-bin/_mt_admin/mt-data-api.cgi/v4/sites/1/entries/${params.id}`
      )
      return {
        post: data,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>
