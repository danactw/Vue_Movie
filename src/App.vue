<script setup>
  import { ref } from 'vue'

  const movieData = ref([])

  fetch('https://top-250-movies.herokuapp.com/api/v1/movies/top')
    .then(res => res.json())
    .then(data => {
      movieData.value = data
    })


</script>

<template>
  <div class="navbar">
    <div class='nav-container'>
      <div>
        <a class="logo" href="#">5x<span>Movies</span></a>
      </div>
      <form class="search-field">
        <input type="text" class="search-term" placeholder="請搜尋...">
        <button type="submit" class="search-button">搜尋</button>
      </form>
    </div>
  </div>

  <div class='content'>
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
        <tr v-for="movie in movieData" :key="movie">
          <td> {{ movie.rank }} </td>
          <td><a href="連結">{{ movie.title }}</a></td>
          <td> {{ movie.year }} </td>
          <td> {{ movie.director }} </td>
          <td> {{ movie.main_stars }} </td>
          <td> {{ movie.rating }} </td>
        </tr> 
      </tbody>
    </table>
    <div class="pagination-container">
      <!-- 
      <span class="back-page">＜</span>
      <div class="pagination">
        <span>1</span>
        <span>2</span>
        <span>3</span>
      </div>
      <span class="next-page">＞</span>
      <div class="pagination-counter">
      </div> 
      -->
    </div>
  </div>
  <footer>
    <p>5xCampus © 2021 Ruby on Rails</p>
  </footer>
</template>

<style>
@import './assets/main.css';

</style>