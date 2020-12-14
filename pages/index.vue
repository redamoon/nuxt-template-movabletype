<template>
  <div>
    <h2 class="title is-3">記事の更新確認</h2>
    <div v-for="(post, index) in posts" :key="index" class="panel">
      <div class="panel-block">{{ post.title }}</div>
    </div>
    <h2 class="title is-3">ウェブページの更新確認</h2>
    <div v-for="(post2, index) in pages" :key="index" class="panel">
      <div class="panel-block">{{ post2.title }}</div>
    </div>
    <h2 class="title is-3">コンテンツタイプの更新確認</h2>
    <div v-for="(post3, index) in content_data" :key="index" class="panel">
      <div class="panel-block">{{ post3.label }}</div>
    </div>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  async asyncData({ $axios, error }) {
    try {
      const entries = await $axios.get(
        'https://movabletype-knowledge.tech/cgi-bin/_mt_admin/mt-data-api.cgi/v4/sites/2/entries'
      )
      const pages = await $axios.get(
        'https://movabletype-knowledge.tech/cgi-bin/_mt_admin/mt-data-api.cgi/v4/sites/2/pages'
      )
      const contentData = await $axios.get(
        'https://movabletype-knowledge.tech/cgi-bin/_mt_admin/mt-data-api.cgi/v4/sites/2/contentTypes/3/data'
      )
      return {
        posts: entries.data.items,
        pages: pages.data.items,
        content_data: contentData.data.items,
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
}
</script>
