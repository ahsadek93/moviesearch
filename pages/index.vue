<template>
  <div class="container">
    <AppHeader />
    <div class="row justify-content-center">
      <AppSearchBox @SearchClicked="passingSearchKeyword" />
    </div>
    <div class="row justify-content-center">
        <AppMovieGrid />
    </div>
  </div>
</template>

<script>
import AppHeader from './../components/AppHeader'
import AppSearchBox from './../components/AppSearchBox'
import AppMovieGrid from './../components/AppMovieGrid'
import {eventBus} from './../plugins/eventBus'

import axios from '@nuxtjs/axios'

let config = {
  headers: {
    'x-rapidapi-host': 'imdb8.p.rapidapi.com',
    'x-rapidapi-key': '5cf97a8b10msh1231c8c16e36af6p125923jsn1f71ac273f25',
  },
}

export default {
  components: {
    AppHeader,
    AppSearchBox,
    AppMovieGrid,
  },

  data() {
    return {
      searchKeyword: '',
      searchResults: ['']
    }
  },

  methods: {
    passingSearchKeyword(value) {
      this.searchKeyword = value
      this.getSearchResults()
    },

    getSearchResults() {
      this.$axios.get('https://imdb8.p.rapidapi.com/title/auto-complete?q=' + this.searchKeyword, config).then((res)=> {
          this.searchResults = res.data.d
          console.log(this.searchResults)
      }).catch((err)=>{
          console.log(err)
      })
    },
  },

  watch: {
      searchResults(){
          eventBus.$emit('searchResultsData', this.searchResults)
      }
  }



}
</script>
