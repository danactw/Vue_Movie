<script setup>
const props = defineProps({
  rank: String,
  title: String,
  year: String,
  director: String,
  main_stars: String,
  rating: String
})

</script>

<template>
  <tr>
    <td> {{ rank }} </td>
    <td><a href="連結">{{ title }}</a></td>
    <td> {{ year }} </td>
    <td> {{ director }} </td>
    <td> {{ main_stars }} </td>
    <td> {{ rating }} </td>
  </tr> 
</template>