<script setup>
  import { computed, ref, watch } from 'vue'

  const movieData = ref([])
  const currentPage = ref(1)
  const dataPerPage = ref(12)
  const searchInput = ref('')
  const totalPage = computed(()=>Math.ceil(movieData.value.length/dataPerPage.value))
  const firstDataPerPage = computed(()=>(currentPage.value-1)*12)
  const lastDataPerPage = computed(()=>currentPage.value*12)
  const slicedData = computed(()=>movieData.value.slice(firstDataPerPage.value, lastDataPerPage.value))

  const displayedPage = computed(()=>{
    if (currentPage.value === 1) return 3;
    if (currentPage.value === 2) return 4;
    if (currentPage.value >= 3) return 5;  
  })

  const offsetPage = computed(()=>{
    return currentPage.value < 3 ? 0 : currentPage.value - 3
  })

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
        <input v-model="searchInput" type="text" class="search-term" placeholder="請搜尋...">
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
        <tr v-for="movie in slicedData" :key="movie">
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
      <span class="back-page" v-if="currentPage !== 1" @click="currentPage--" >＜</span>
      <div class="pagination">
        <template v-for="page in displayedPage" :key="page">
          <span @click="currentPage = page + offsetPage"
                :class="(page + offsetPage) === currentPage ? 'active' : '' "
                v-if="page + offsetPage <= totalPage"
          > {{ page + offsetPage }} </span>
        </template>
      </div>
      <span class="next-page" v-if="currentPage !== totalPage" @click="currentPage++" >＞</span>
      <div class="pagination-counter">
      </div> 
    </div>
  </div>

  <footer>
    <p>5xCampus © 2021 Ruby on Rails</p>
  </footer>
</template>

<style>
@import './assets/main.css';

</style>