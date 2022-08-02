<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editProductParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.editProductParams = response.data;
    });
  },
  methods: {
    updateProduct: function () {
      axios
        .patch("/products/" + this.$route.params.id + ".json", this.editProductParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/products");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="products-edit">
    <form v-on:submit.prevent="updateProduct()">
      <h1>Update Product</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>
        Name:
        <input type="text" v-model="editProductParams.name" />
      </p>
      <p>
        Description:
        <input type="text" v-model="editProductParams.description" />
      </p>
      <p>
        Image:
        <input type="text" v-model="editProductParams.image" />
      </p>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
