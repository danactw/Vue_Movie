<script>
  import { computed } from "vue"
  export default {
    props: {
      currentPage: Number,
      totalPage: Number
    },
    setup(props, {emit}) {
      const setPage = val => {
        emit('updateCurrentPage', val)
      }

      const displayedPage = computed(()=>{
        if (props.currentPage === 1) return 3;
        if (props.currentPage === 2) return 4;
        if (props.currentPage >= 3) return 5;  
      })

      const offsetPage = computed(()=>{
        return props.currentPage < 3 ? 0 : props.currentPage - 3
      })

      return{
        setPage,
        displayedPage,
        offsetPage
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