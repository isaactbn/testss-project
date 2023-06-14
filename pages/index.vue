<template>
  <v-container>
    <v-data-table
      v-model="news"
      :headers="headers"
      :items="news"
      item-key="author"
      class="elevation-1"
      hide-default-footer
      disable-pagination
      disable-sort
    >
      <!-- eslint-disable-next-line -->
      <template v-slot:header.author >
        <button>
          Author
        </button>
      </template>
      <!-- eslint-disable-next-line -->
      <template v-slot:header.content >
        <button>
          Content
        </button>
      </template>
      <!-- eslint-disable-next-line -->
      <template v-slot:header.description >
        <button>
          Description
        </button>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'IndexPage',
  data() {
    return {
      news: [],
      headers: [
        { text: 'Author', value: 'author', class: 'text--disabled', width: '90px' },
        { text: 'Content', value: 'content', class: 'text--disabled', width: '180px' },
        { text: 'Description', value: 'description', class: 'text--disabled', width: '340px' },
      ]
    };
  },
  created() {
    this.getNews()
  },
  methods: {
    async getNews() {
      const resp = await axios.get('https://newsapi.org/v2/everything?q=tesla&from=2023-05-14&sortBy=publishedAt&apiKey=a09ad5ff23f64fde8f66201265090c46')
      this.news = resp.data.articles
    }
  }
}
</script>
