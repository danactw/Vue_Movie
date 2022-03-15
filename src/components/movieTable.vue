<script>
import TableRow from "./tableRow.vue";
  export default {
    props: {
        slicedData: Array,
    },
    components: { TableRow }
}
</script>

<template>
  <table class="styled-table">
    <thead>
      <tr>
        <th>排名</th>
        <th>片名</th>
        <th>年份</th>
        <th>導演</th>
        <th>主要演員</th>
        <th>評分</th>
      </tr>
    </thead>
    <tbody>
      <TableRow v-for="movie in slicedData" :key="movie" v-bind="movie" />
      <!-- <tr v-for="movie in slicedData" :key="movie">
        <td> {{ movie.rank }} </td>
        <td><a href="連結">{{ movie.title }}</a></td>
        <td> {{ movie.year }} </td>
        <td> {{ movie.director }} </td>
        <td> {{ movie.main_stars }} </td>
        <td> {{ movie.rating }} </td>
      </tr>  -->
    </tbody>
  </table>
  <div v-if="slicedData.length===0" >很抱歉！目前沒有您搜尋的電影！</div>
</template>

<style>

</style>