<template>
  <v-container>
    <v-container>
      <h1 style="font-family: Nunito, sans-serif;">PRODUTOS</h1>
    </v-container>
    <hr>
    <v-container>
      <v-row
        style="margin-top: 1%"
        :key="i">
        <v-col 
          cols="4"
          v-for="(product, i) in products"
          :key="i">
          <v-card
            class="mx-auto"
            max-height="500">
            <v-img
              height="300"
              widht="500 "
              :src="product.imageLink"></v-img>
            <v-card-title>{{ product.name }}</v-card-title>
            <v-card-subtitle>Categoria: {{ product.category.name }}</v-card-subtitle>
            <v-cart-text align="center">
              <v-row
                align="center"
                class="mx-0">
                <v-col>
                  <v-rating
                    :value="4.5"
                    color="yellow"
                    dense
                    half-increments
                    readonly
                    size="14"
                  ></v-rating>
                </v-col>
              </v-row>
              <v-row
                align="center"
                class="mx-0"
              >
                <v-col>
                  <div>R$ {{ product.price }}</div>
                </v-col>
              </v-row>
            </v-cart-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'storePage',
  layout: 'default',
  data() {
    return {
      categories: [],
      products: []
    }
  },

  created() {
    this.get();
  },

  methods: {
    async get() {
      let products = await this.$api.get('/products').then(res => res.data)
      let categories = await this.$api.get('/categories').then(res => res.data)
      this.categories = categories
      this.products = products
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito');
</style>