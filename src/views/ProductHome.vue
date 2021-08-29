<template>
  <div class="container mt-5">
    <div class="row">
      <h1 v-if="loading">Loading ...</h1>
      <div class="col-md-4 mb-4" v-for="product in products" :key="product.id">
        <div class="card">
          <div class="card-body text-center">
            <img :src="product.image" alt="Product Image" class="p-img" />
            <h4 class="mt-4">
              {{ product.title }}
            </h4>
            <p class="my-4 text-muted">$ {{ product.price }}</p>
            <router-link
              class="btn btn-primary btn-block"
              :to="`/product/${product.id}`"
              >More Detail</router-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "ProductHome",
  data() {
    return {
      loading: false,
      products: [],
    };
  },
  created() {
    this.loading = true;
    axios
      .get("https://fakestoreapi.com/products")
      .then((response) => {
        console.log(response.data);
        this.products = response.data;
        this.loading = false;
      })
      .catch((e) => {
        this.loading = false;
      });
  },
};
</script>
<style>
.p-img {
  height: 150px;
}
</style>
