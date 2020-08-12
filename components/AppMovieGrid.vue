<template>
  <div v-if="gotData" class="col-12 card">
    <div class="row justify-content-center">
      <AppMovieCard
        v-for="result in searchResultsData"
        v-bind:key="result.id"
        :card-data="result"
      />
    </div>
  </div>
</template>

<script>
import { eventBus } from './../plugins/eventBus'
import AppMovieCard from './AppMovieCard'
export default {
  components: {
    AppMovieCard,
  },
  data() {
    return {
      searchResultsData: [''],
      gotData: false,
    }
  },

  mounted() {
    eventBus.$on('searchResultsData', (data) => {
      this.searchResultsData = data
      this.gotData = true
    })
  },
}
</script>

<style></style>
