<template>
  <div class="bg-white max-w-3xl m-auto p-8 rounded-xl">
    <template v-if="isLoading">
      <div>
        <vue-feather
          type="loader"
          animation="spin"
          animation-speed="fast"
          :stroke="activeColor"
        ></vue-feather>
      </div>
    </template>
    <template v-else-if="isSuccess">
      <div class="text-3xl" :style="{ color: activeColor }">
        {{ data.content }}
      </div>
      <div class="text-right text-sm mb-3" :style="{ color: activeColor }">
        - {{ data.author }}
      </div>
    </template>
    <template v-else-if="isError">
      <div class="text-3xl" :style="{ color: activeColor }">
        Something went wrong
      </div>
    </template>
    <button
      class="text-white text-center py-1.5 px-3 rounded border border-transparent inline-flex items-center"
      :style="{ background: activeColor }"
      @click="fetchQuote()"
    >
      <span class="pr-1 inline-flex items-center">
        <vue-feather type="refresh-cw" size="16"></vue-feather>
      </span>
      New Quote
    </button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'QuoteBox',
  props: {
    activeTags: Array,
    activeColor: String,
  },
  data() {
    return {
      status: 'idle',
      data: null,
    }
  },
  computed: {
    isLoading() {
      return this.status === 'loading' || this.status === 'idle'
    },
    isError() {
      return this.status === 'error'
    },
    isSuccess() {
      return this.status === 'success'
    },
    isIdle() {
      return this.status === 'idle'
    },
  },
  methods: {
    async fetchQuote(tags = []) {
      this.status = 'loading'
      try {
        const res = await axios.get('https://api.quotable.io/random', {
          params: {
            tags: tags.join(','),
          },
        })
        this.status = 'success'
        this.data = {
          content: res.data.content,
          author: res.data.author,
        }
      } catch (err) {
        this.status = 'error'
      }
    },
  },
  watch: {
    activeTags(newActiveTags) {
      this.fetchQuote(newActiveTags)
    },
  },
  mounted() {
    this.fetchQuote()
  },
}
</script>

<style scoped></style>
