<template>
  <v-container>
    <v-row class="text-center">
      <v-col
        cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Login
        </h2>
        <v-card
          class="mx-auto"
          max-width="344"
          outlined
          :loading="loading"
        >

          <v-card-text>
            <login-form @success="onSuccess" />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import LoginForm from "../components/LoginForm.vue";
  export default {
    name: 'LoginPage',
    components: { LoginForm },
    data: () => ({
      loading: true,
    }),
    methods: {
      onSuccess () {
        this.$router.push('products')
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
