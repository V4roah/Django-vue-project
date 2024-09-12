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
    <hr />
    <h6>REACTIVIDAD LOS DATOS QUE SE MUESTRAN EN LA VISTA CAMBIA</h6>
    <p>La variables 'prueba' vale {{ prueba }}</p>

    <h5>
      contador <strong>{{ contador }}</strong>
    </h5>
    <button class="btn btn-sm btn-success" @click="incrementar">
      INCREMENTAR
    </button>
    <button class="btn btn-sm btn-warning" @click="decrementar">
      DECREMENTAR
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const hacerClick = (mensaje) => {
  console.log(mensaje);
};

const queBotonPresiono = (mensaje) => {
  console.log(mensaje);
};

const incrementar = () => {
  contador.value++;
};

const decrementar = () => {
  contador.value <= 0 ? (contador.value = 0) : contador.value--;
};

const prueba = 0;

let contador = ref(0);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialised;
  -moz-osx-font-smoothing: graysclase;
  margin-top: 60px;
}
</style>
