<template>
<layout-wrapper>
  <layout-visual
      title="Information"
      :height="40"
      visual="visual-information"
       />

  <div class="w-full md:max-w-3xl mx-auto pt-20">
    <h2 class="text-xl pb-5 border-b border-gray-500 border-solid font-bold">
      {{ item.title }}
    </h2>
    <div class="pt-4 mb-4">
      <time class="text-gray-700 yrxt-base">{{ item.date | formatDate }}</time>
    </div>
    <div class="mb-20" v-html="item.body">
    </div>
    <base-button name="お知らせへ戻る" link="/information/" />
  </div>
</layout-wrapper>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ $config, params, error }) {
    try {
      const { data } = await axios.get(
        `${$config.apiUrl}/information/${params.id}`,
        {
          headers: { 'X-MICROCMS-API-KEY': $config.apiKey }
        }
      )
      return {
        item: data
      }
    } catch (err) {
      error({
        errorCode: 404,
      })
    }
  },
  head() {
    return {
      title: this.item.title
    }
  }
}
</script>

