<template>
  <v-container>
    <v-row class="text-center">
      <v-col
        cols="12"
      >
        <v-skeleton-loader
          v-if="!products.length"
          class="mx-auto"
          type="card"
        />
        <v-row v-else justify="center">
          <v-card
            v-for="(product, i) in products"
            :key="i"
            class="mb-10 mr-5 product-image"
          >
            <v-img
              class="white--text align-end"
              height="200px"
              :src="product.thumbnail"
            >
              <v-card-title>{{ product.name }}</v-card-title>
            </v-img>

            <v-card-subtitle class="pb-0">
              {{ product.price }}$
            </v-card-subtitle>

            <v-card-text class="text--primary">
              <div>{{ product.description }}</div>
            </v-card-text>

            <v-card-actions>
              <v-btn
                color="orange"
                text
              >
                Buy
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'Products',

    data: () => ({
      products: []
    }),

    async created () {
      // todo: move request to beforeRoute, response processing to service and state to vuex
      // todo: handle errors and check failure path
      try {
        const response = await fetch('https://dummyjson.com/products')
        this.products = (await response.json()).products
      } catch (e) {
        console.error(e)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .product-image {
    max-width: 100%;
    @media (min-width: 1024px) {
      max-width: 30%;
    }
  }
</style>
