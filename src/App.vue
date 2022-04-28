<template>
  <div class="h-screen text-center" :style="{ background: activeColor }">
    <div class="text-white text-5xl py-16">Random Quote Machine</div>
    <quote-box :activeColor="activeColor" :activeTags="activeTagArr" />
    <div class="mt-4">
      <color-picker
        :activeColor="activeColor"
        @onChangeActiveColor="changeActiveColor"
      />
    </div>
    <div class="mt-4">
      <tag-box @onToogleActiveTag="toogleActiveTag" :activeTags="activeTags" />
    </div>
  </div>
</template>

<script>
import QuoteBox from '@/components/QuoteBox.vue'
import ColorPicker from './components/ColorPicker.vue'
import TagBox from './components/TagBox.vue'

export default {
  name: 'App',
  components: {
    QuoteBox,
    ColorPicker,
    TagBox,
  },
  data() {
    return {
      activeColor: 'indianred',
      activeTags: {},
    }
  },
  computed: {
    activeTagArr() {
      return Object.keys(this.activeTags).filter((tag) => this.activeTags[tag])
    },
  },
  methods: {
    changeActiveColor(newActiveColor) {
      this.activeColor = newActiveColor
    },
    toogleActiveTag(tag) {
      this.activeTags[tag] = !this.activeTags[tag]
    },
  },
}
</script>

<style>
body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

code {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}
</style>
