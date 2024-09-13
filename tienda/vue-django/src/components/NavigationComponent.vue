<template>
  <section class="mt-5 text-center mx-auto">
    <h1 class="text-danger">Panadería y Rotisería Carlitos</h1>
    <img class="img-fluid img-personalizada" :src="fondoImage" alt="" />
    <div class="mt-3" v-if="$route.path !== '/about'">
      <button
        type="button"
        class="btn btn-warning"
        v-for="category in categories"
        :key="category - id"
        @click="getCategory(category.id, category.name)"
      >
        {{ category.name }}
      </button>
    </div>
    <hr />
  </section>
</template>

<script setup>
import axios from "axios";
import fondoImage from "@/assets/img/fondo.jpg";
import { ref, defineEmits, onMounted } from "vue";

const categories = ref([]);
const categoryId = ref(null);
const categoryName = ref(null);

const emit = defineEmits(["getCategoryId"]);

const getCategory = (id, name) => {
  emit("getCategoryId", id, name);
};

onMounted(() => {
  axios
    .get("http://localhost:8000/api/v1.0/categories/")
    .then((response) => {
      categories.value = response.data;
    })
    .catch((error) => {
      console.log(error);
    });
});
</script>

<style>
.img-personalizada {
  width: 800px;
  height: 400px;
  object-fit: cover;
}
button {
  margin-right: 5px;
}

button + button,
button:first-child {
  margin-left: 5px;
}
@media (max-width: 768px) {
  button {
    width: 100%;
    margin: 0 0 5px !important;
    box-sizing: border-box;
  }
}
</style>
