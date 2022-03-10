<script setup>
  import { computed, ref, watch } from 'vue'
  import PageFooter from './components/pageFooter.vue'
  import Search from './components/search.vue'
  import MovieTable from './components/movieTable.vue'

  const movieData = ref([])
  const currentPage = ref(1)
  const dataPerPage = ref(12)
  const searchInput = ref('')
  const totalPage = computed(()=>Math.ceil(searchedData.value.length/dataPerPage.value))
  const firstDataPerPage = computed(()=>(currentPage.value-1)*12)
  const lastDataPerPage = computed(()=>currentPage.value*12)
  const slicedData = computed(()=>searchedData.value.slice(firstDataPerPage.value, lastDataPerPage.value))

  const searchedData = computed(()=>{
    if (searchInput.value === '') {
      return movieData.value
    } else {
      return movieData.value.filter((movie)=>movie.title.includes(searchInput.value))
    }
  })

  watch(()=>searchInput.value, ()=>currentPage.value = 1)

  const setSearchInput = (val) => {searchInput.value = val}

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
      <Search :searchInput="searchInput" @updateSearch="setSearchInput" />
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

  <div v-if="searchedData.length===0" >很抱歉！目前沒有您搜尋的電影！</div>
  <PageFooter />
</template>

<style>
@import './assets/main.css';

</style>