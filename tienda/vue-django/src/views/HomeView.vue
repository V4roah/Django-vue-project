<template>
  <!-- NAVBAR -->
  <NavbarComponent @getSearchText="search" />

  <!-- navigation -->
  <NavigationComponent @getCategoryId="categoryId" />

  <div class="mb-3" v-if="searchTextRule">
    <h3>
      Productos de la categoria <strong>{{ searchTextRule }}</strong>
    </h3>
    <button class="btn btn-lg btn-warning" @click="resetFilter">
      Mostrar todas las categorias
    </button>
    <div
      class="alert alert-danger mt-3"
      role="alert"
      v-if="filteredProducts.length === 0"
    >
      No existen productos con el texto
      <strong>{{ searchTextRule }}</strong>
    </div>
  </div>

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

<script setup>
import axios from "axios";
import NavigationComponent from "@/components/NavigationComponent.vue";
import NavbarComponent from "@/components/NavbarComponent.vue";
import { ref, onMounted } from "vue";

const products = ref([]);
const filteredProducts = ref([]);
const categoryReceived = ref(null);
const searchTextRule = ref(null);

const search = (searchText) => {
  categoryReceived.value = null;
  searchTextRule.value = searchText;
  // console.log("busqueda desde el homeview", searchTextRule.value);

  if (searchText) {
    filteredProducts.value = products.value.filter((product) => {
      const productName = product.name.toLowerCase();
      const productDescription = product.description.toLowerCase();
      const searchTerm = searchText.toLowerCase();

      return (
        productName.includes(searchTerm) ||
        productDescription.includes(searchTerm)
      );
    });
  } else {
    filteredProducts.value = products.value;
  }
};

const categoryId = (categoryId, categoryName) => {
  searchTextRule.value = null;

  categoryReceived.value = categoryName;
  if (categoryId) {
    filteredProducts.value = products.value.filter(
      (product) => product.category === categoryId
    );
  } else {
    filteredProducts.value = products.value;
  }
};

const resetFilter = () => {
  categoryReceived.value = null;
  searchTextRule.value = null;
  filteredProducts.value = products.value;
};

onMounted(() => {
  axios
    .get("http://localhost:8000/api/v1.0/products/")
    .then((response) => {
      products.value = response.data;
      filteredProducts.value = products.value;
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>

<style>
.card {
  border: 2px solid gray !important;
}
</style>
