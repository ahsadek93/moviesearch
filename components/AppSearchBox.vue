<template>
  <div class="col-10 col-md-12 my-4 card p-3">
    <div class="row justify-content-center text-center">
      <div class="col-12">
        <h2>Welcome to Movies Online Store</h2>
      </div>
      <div class="col-12">
        <p class="m-0">One site to collect them all, One Site to find them.</p>
      </div>
      <div class="col-12">
        <p class="m-0">
          One site to bring them all, And on your collection binds them.
        </p>
      </div>
      <div class="col-12 my-4">
        <div class="row justify-content-center">
          <b-form class="col-11 col-md-6">
            <b-form-group
              id="input-group-1"
              label-for="input-1"
              description="Search for your favourite movie."
            >
              <div class="row justify-content-between">
                <div class="col-12 text-left" v-if="searchBoxEmpty">
                  <p class="m-0 text-danger">Search box cannot be empty!</p>
                </div>
                <b-form-input
                  class="col mx-3"
                  id="input-1"
                  type="text"
                  required
                  placeholder="Enter Movie name here"
                  v-model="searchKeyword"
                ></b-form-input>
                <button class="btn btn-info" @click="passingSearchValue">
                  Search
                </button>
              </div>
            </b-form-group>
          </b-form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchKeyword: '',
      searchBoxEmpty: false,
    }
  },

  methods: {
    passingSearchValue() {
      if (!this.searchKeyword || !this.searchKeyword.trim()) {
        event.preventDefault()
        this.searchBoxEmpty = true
      } else {
        event.preventDefault()
        this.searchBoxEmpty = false
        this.$emit('SearchClicked', this.searchKeyword)
      }
    },


    
  },
}
</script>

<style></style>
