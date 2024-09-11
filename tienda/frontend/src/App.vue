<template>
  <div class="container my-4">
    <h2 class="text-primary">eventos</h2>
    <h6>Botones</h6>
    <button
      class="btn btn-primary"
      v-on:click="hacerClick('mensaje enviado desde la etiqueta azul')"
    >
      Click Aqui
    </button>
    <button
      class="btn btn-success"
      @click="hacerClick('mensaje enviado desde la etiqueta verde')"
    >
      Click Aqui
    </button>
    <hr />
    <h6>MODIFICADORES</h6>
    <button
      class="btn btn-warning"
      @click="queBotonPresiono('Presiono el boton de la izquierda')"
    >
      IZQUIERDA
    </button>
    <button
      class="btn btn-info"
      @click.middle="queBotonPresiono('Boton central')"
    >
      CENTRO
    </button>
    <button
      class="btn btn-success"
      @click.right.prevent="queBotonPresiono('Boton derecho')"
    >
      DERECHO
    </button>
  </div>
</template>

<script setup>
const hacerClick = (mensaje) => {
  console.log(mensaje);
};

const queBotonPresiono = (mensaje) => {
  console.log(mensaje);
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialised;
  -moz-osx-font-smoothing: graysclase;
  margin-top: 60px;
}
</style>
