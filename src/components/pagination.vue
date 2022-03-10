<script>
  export default {
    props: {
      currentPage: Number,
      displayedPage: Number,
      offsetPage: Number,
      totalPage: Number
    },
    setup(props, {emit}) {
      const setPage = val => {
        emit('updateCurrentPage', val)
      }

      return{
        setPage
      }
    }
  }
</script>

<template>
  <div class="pagination-container">
    <span class="back-page" v-if="currentPage !== 1" @click="setPage(currentPage-1)" >＜</span>
    <div class="pagination">
      <template v-for="page in displayedPage" :key="page">
        <span @click="setPage(page+offsetPage)"
              :class="(page + offsetPage) === currentPage ? 'active' : '' "
              v-if="page + offsetPage <= totalPage"
        > {{ page + offsetPage }} </span>
        <!-- @click="currentPage = page + offsetPage" -->
      </template>
    </div>
    <span class="next-page" v-if="currentPage !== totalPage" @click="setPage(currentPage+1)" >＞</span>
    <div class="pagination-counter">
    </div> 
  </div>
</template>

<style>

</style>