<template>
  <div class="container">
    <!-- navbar -->
    <NavBarComponent v-if="$route.path !== '/'" />

    <!-- navigation -->
    <NavigationComponent v-if="$route.path === '/about'" />
    <router-view />

    <!-- footer -->
    <FooterComponent />
  </div>
</template>

<script setup>
import NavBarComponent from "./components/NavbarComponent.vue";
import NavigationComponent from "./components/NavigationComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
