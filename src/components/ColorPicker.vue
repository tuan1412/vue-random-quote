<template>
  <div class="bg-white inline-flex items-center justify-center m-auto p-0.5">
    <template v-for="color in colors" :key="color">
      <span
        @click="$emit('onChangeActiveColor', color)"
        class="cursor-pointer w-8 h-8 m-1"
        :class="{
          'outline outline-2 outline-gray-300 scale-110': color === activeColor,
        }"
        :style="{ background: color }"
      ></span>
    </template>
  </div>
</template>

<script>
export default {
  name: 'ColorPicker',
  emits: ['onChangeActiveColor'],
  props: {
    activeColor: String,
  },
  data() {
    return {
      colors: [
        'cornflowerblue',
        'blueviolet',
        'indianred',
        'deeppink',
        'forestgreen',
      ],
    }
  },
}
</script>

<style></style>
