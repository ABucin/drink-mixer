<script setup lang="ts">
import {ref} from "vue";

const title = ref('Drink Mixer');
</script>

<template>
  <h1>{{title}}</h1>
  <p>
    - app that tells you what cocktails you can make with current booze (+qty)
    --- provide alcohol + other (juice, syrup, water) + quantity
    --- app suggests recipes and highlights overlap (green for valid ingredients, grey/red for missing ones, orange for ones that exist but are insufficient)
    --- can provide natural words (?) (e.g. a bottle, a pinch, a bit, a lot)
  </p>
</template>

<style scoped>

</style>
