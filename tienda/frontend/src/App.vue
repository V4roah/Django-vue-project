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

    <h5>RESULTADO = {{ resultado }}</h5>

    <hr />

    <h6>Variables computadas y objetos</h6>

    <div class="card" style="width: 18rem">
      <img src="#" class="card-img-top" alt="#" />
      <div class="card-body">
        <h5 class="card-title">{{ paisCorregido }}</h5>
        <p class="card-text">{{ paises[contadorPaises].capital }}</p>
        <p class="card-text">{{ paises[contadorPaises].moneda }}</p>
        <p class="text-secondary text-center">
          {{ contadorPaises + 1 }} de {{ totalPaises }}
        </p>
        <button class="btn btn-sm btn-success" @click="anterior">
          Anterior
        </button>
        <button class="btn btn-sm btn-success" @click="siguiente">
          Siguiente
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

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

const valorUnitario = 33.33;

const contador = ref(0);

const resultado = computed(() => {
  let calculo = parseFloat((valorUnitario * contador.value).toFixed(2));
  return calculo + 10;
});

const paises = [
  {
    bandera: "link",
    pais: "Colombia",
    capital: "Bogota",
    moneda: "Peso Colombiano",
  },
  {
    bandera: "link",
    pais: "argentina",
    capital: "Buenos Aires",
    moneda: "Peso Argentino",
  },
  {
    bandera: "link",
    pais: "Mexico",
    capital: "Ciudad de Mexico",
    moneda: "Peso Mexicano",
  },
];

const contadorPaises = ref(0);
const totalPaises = paises.length;

const siguiente = () => {
  contadorPaises.value++;
  if (contadorPaises.value >= totalPaises) {
    contadorPaises.value = 0;
  }
};

const anterior = () => {
  if (contadorPaises.value <= 0) {
    contadorPaises.value = totalPaises;
  }
  contadorPaises.value--;
};

const paisCorregido = computed(() => {
  const paisOriginal = paises[contadorPaises.value].pais.toLowerCase();

  return paisOriginal.substring(0, 1).toUpperCase() + paisOriginal.substring(1);
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialised;
  -moz-osx-font-smoothing: graysclase;
  margin-top: 60px;
}
</style>
