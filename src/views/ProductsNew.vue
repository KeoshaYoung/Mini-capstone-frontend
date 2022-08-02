<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "New Product",
      newProductParams: {},
      errors: [],
    };
  },
  methods: {
    createProduct: function () {
      axios
        .post("/Products.json", this.newProductParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/Products");
          this.newProductParams = "";
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="Products-new">
    <form v-on:submit.prevent="createProduct()">
      <h1>{{ message }}</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="newProductParams.name" />
        <label>Description:</label>
        <input type="text" v-model="newProductParams.body" />
        <label>Image:</label>
        <input type="text" v-model="newProductParams.image" />
      </div>
      <button v-on:click="createProduct">Create</button>
    </form>
  </div>
</template>
