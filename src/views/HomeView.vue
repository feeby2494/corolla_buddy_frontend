<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">
          Welcome to Corolla Buddy
        </p>
        <p class="subtitle">
          Corolla is the number one car in the world!
        </p>
      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Products</h2>
      </div>

      <div class="columns is-multiline">
            <ProductBox 
            
            v-for="product in latestProducts"
            v-bind:key="product.id"
            :product="product">
            </ProductBox>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from '@/components/ProductBox.vue'

export default {
  name: 'HomeView',
  data() {
    return {
      latestProducts: []
    }
  },
  components: { 
    ProductBox
  },
  mounted() {
    this.getLatestProducts()

    document.title = 'Home'+ ' - Corolla Buddy'
  },
  methods: {
    async getLatestProducts() {
      
      this.$store.commit('setIsLoading', true)

      await axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts = response.data
        })
        .catch(error => {
          console.log(error)
        })
        this.$store.commit('setIsLoading', false)
    }
  }
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }
</style>
