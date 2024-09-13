<template>
  <!-- navigation -->
  <NavigationComponent @getCategoryId="categoryId" />
  <div class="mb-3" v-if="categoryReceived">
    <h3>
      Productos de la categoria <strong>{{ categoryReceived }}</strong>
    </h3>
    <button class="btn btn-lg btn-warning" @click="resetFilter">
      Mostrar todas las categorias
    </button>
    <div
      class="alert alert-danger mt-3"
      role="alert"
      v-if="filteredProducts.length === 0"
    >
      No existen productos para la categoria
      <strong>{{ categoryReceived }}</strong>
    </div>
  </div>
  <div class="container">
    <div>
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col" v-for="product in filteredProducts" :key="product.id">
          <div class="card text-center">
            <img
              :src="product.image"
              class="card-img-top"
              :alt="product.name"
            />
            <div class="card-body">
              <h5 class="card-title">{{ product.name }}</h5>
              <h6 class="card-subtitle mb-2 text-body-secondary">
                {{ product.category_name }}
              </h6>
              <p class="card-text">{{ product.description }}</p>
            </div>
            <div class="card-footer text-danger">
              {{ product.price }} - Por {{ product.price_type_description }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import NavigationComponent from "@/components/NavigationComponent.vue";

export default {
  components: {
    NavigationComponent,
  },
  name: "HomeView",
  data() {
    return {
      products: [],
      filteredProducts: [],
      allProducts: [],
      categoryReceived: null,
    };
  },

  methods: {
    categoryId(categoryId, categoryName) {
      this.categoryReceived = categoryName;
      if (categoryId) {
        this.filteredProducts = this.allProducts.filter(
          (product) => product.category === categoryId
        );
      } else {
        this.filteredProducts = this.allProducts;
      }
    },
    resetFilter() {
      this.categoryReceived = null;
      this.filteredProducts = this.allProducts;
    },
  },
  mounted() {
    axios
      .get("http://localhost:8000/api/v1.0/products/")
      .then((response) => {
        this.allProducts = response.data;
        this.filteredProducts = this.allProducts;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
.card {
  border: 2px solid gray !important;
}
</style>
