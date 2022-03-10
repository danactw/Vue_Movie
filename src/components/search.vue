<script setup>
  import { watch } from 'vue'

  const props = defineProps({
    searchInput: String,
  })

  const emit = defineEmits(['updateSearch'])

  watch(()=>props.searchInput, (val)=> {
    emit('updateSearch', val)
  })

</script>

<template>
  <form class="search-field">
    <input v-model="searchInput" type="text" class="search-term" placeholder="請搜尋...">
    <button type="submit" class="search-button">搜尋</button>
  </form>
</template>

<style>

</style>