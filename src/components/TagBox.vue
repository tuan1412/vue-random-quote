<template>
  <div class="flex flex-wrap justify-center">
    <template v-for="tag in tags" :key="tag">
      <span
        @click="$emit('onToogleActiveTag', tag)"
        class="bg-white p-1 m-1 cursor-pointer"
        :class="{ 'text-white bg-yellow-600': activeTags[tag] }"
        >{{ tag }}</span
      >
    </template>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TagBox',
  emits: ['onToogleActiveTag'],
  props: {
    activeTags: Object,
  },
  data() {
    return {
      tags: [],
    }
  },
  mounted() {
    axios.get('https://api.quotable.io/tags').then((res) => {
      this.tags = res.data.map((tag) => tag.name)
    })
  },
}
</script>

<style lang="scss" scoped></style>
