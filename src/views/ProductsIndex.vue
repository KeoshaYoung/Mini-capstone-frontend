<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Products",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/products.json").then((response) => {
        this.products = response.data;
        console.log("All products:", this.products);
      });
    },
  },
};
</script>

<template>
  <h1>{{ message }}</h1>
  <div v-for="product in products" v-bind:key="product.id">
    <router-link v-bind:to="`/products/${product.id}`">
      <h3>{{ product.name }}</h3>
    </router-link>
    <img :src="product.image" alt="" />
    <p>
      {{ product.description }}
    </p>
  </div>
</template>
