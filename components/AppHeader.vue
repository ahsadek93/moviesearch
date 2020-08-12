<template>
  <b-navbar type="dark" variant="info">
    <b-navbar-brand href="#">BuyMovies</b-navbar-brand>

    <b-navbar-nav class="ml-auto">
      <b-nav-item href="#">
        <a class="text-white" v-b-modal.modal-1>
          <i class="fa fa-shopping-cart"></i>
        </a>
      </b-nav-item>
    </b-navbar-nav>

    <b-modal id="modal-1" title="Cart Items">
      <div class="row justify-content-center">
        <div class="col-10">
          <div
            class="row justify-content-center card flex-row p-2 my-2"
            v-for="(item, index) in cartItems"
            v-bind:key="item.id"
          >
            <div class="col-10 col-md-4">
              <img
                :src="item.img"
                alt="movieimg"
                class="img-card-top img-fluid"
              />
            </div>
            <div class="col align-self-center">{{ item.title }}</div>
            <div class="align-self-center">
              <a href="#" class="btn btn-danger" @click="removeItem(index)"
                ><i class="fa fa-trash"></i
              ></a>
            </div>
          </div>
        </div>
      </div>
      <div slot="modal-footer">
        <b-button size="sm" variant="success">Check Out</b-button>
        <b-button size="sm" variant="danger" @click.prevent="removeAllItems()">Empty cart</b-button
        >
      </div>
    </b-modal>
  </b-navbar>
</template>

<script>
import { eventBus } from './../plugins/eventBus'

export default {
  mounted() {
    eventBus.$on('addMovieToCart', (data) => {
      this.cartItems.push(data)
      console.log(this.cartItems)
    })
  },
  data() {
    return {
      cartItems: [],
    }
  },

  methods: {
    removeItem(index) {
      this.cartItems.splice(index, 1)
    },
    removeAllItems() {
        this.cartItems = [];
        console.log(this.cartItems)
    }
  },
  
}
</script>

<style></style>
