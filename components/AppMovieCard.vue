<template>
  <div class="col-10 col-md-6 col-lg-4 p-4" v-if="cardData.q === `feature`">
    <div class="row h-100">
      <div class="col-12 p-2 text-center card">
        <div class="img-container">
          <img
            :src="cardData.i.imageUrl"
            alt="movieCover"
            class="card-img-top"
          />
        </div>
        <div class="card-body text-center">
          <h5 class="card-title">{{ cardData.l }}</h5>
          <div class="card-text">
            <div class="row">
              <div class="col-12">
                <span class="text-info mx-1">IMDB Rank</span
                ><span>{{ cardData.rank }}</span>
              </div>
              <div class="col-12">
                <span class="text-info mx-1">Year</span
                ><span>{{ cardData.y }}</span>
              </div>
              <div class="col-12">
                <span class="text-info mx-1">Starring</span
                ><span>{{ cardData.s }}</span>
              </div>
            </div>
          </div>
          <p class="card-text">
            <small class="text-info"><a href="#" @click="addToCart">Add to Cart</a></small>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from './../plugins/eventBus'


export default {
  props: {
    cardData: {
      type: Object,
    },
  },

  data(){
      return{
          movieInfo: {
              title:'',
              img:'',
              id:''
          }
      }
  },
  created() {
    if (this.cardData.i === null || this.cardData.i === undefined) {
      this.cardData.i = {}
      this.cardData.i.imageUrl =
        'https://upload.wikimedia.org/wikipedia/commons/0/0a/No-image-available.png'
    }
  },

  methods: {
      addToCart() {
          this.movieInfo.title = this.cardData.l;
          this.movieInfo.img = this.cardData.i.imageUrl;
          this.movieInfo.id = this.cardData.id
          eventBus.$emit('addMovieToCart', this.movieInfo);
      }
  }
}
</script>

<style>
.img-container {
  position: relative;
  padding-top: 100%;
}

.card-img-top {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: center;
}
</style>
