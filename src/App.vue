<script setup>
import { ref, computed } from 'vue'

const name = "vue dinámico";
const styleColor = "color: blue";
const arrayColores = ["blue", "red", "white"];

//ref constantes
const arrayFavoritos = ref([])
let counter = ref(0);

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value)
  return numSearch || numSearch === 0
})

//métodos
const aumentarContador = () => counter.value++

const disminuirContador = () => counter.value--

const resetearContador = () => (counter.value = 0)

const add = () => {
  arrayFavoritos.value.push(counter.value)
}

const nuevoArray = [
  {
    name: "manzana",
    price: "$1.00",
    descripcion: "una manzana",
    stock: 10
  },
  {
    name: "pera",
    price: "$2.00",
    descripcion: "una pera",
    stock: 20
  },
];
const objetoFruta = {
  id: 1,
  name: "manzana",
  price: "$1.00",
  descripcion: "una manzana",
}
const activo = false;

//metodo - methods
const hacerClick = () => {
  console.log("Hiciste Click")
}

</script>

<template>
  <h1>Hola Vue.js</h1>
  <h2 :style="styleColor">Llamando a {{ name.toUpperCase() }} y cambiando el color con v-bind</h2>
  <h3 :style="`color: ${arrayColores[1]}`">{{ arrayColores }}</h3>
  <h4>{{ activo ? "Tamo activo" : "No tamo activo" }}</h4>
  <p v-if="activo">estamo recontra activo</p>
  <p v-else="!activo">no se que poner</p>
  <h2 v-show="activo">el v-show me va a desaparecer</h2>

  <ul>
    <li v-for="color, index in arrayColores" :key="index">
      {{ color.toUpperCase() }} - {{ index }}
    </li>
  </ul>

  <ul>
    <template v-for="fruta in nuevoArray" :key="fruta.name">
      <li v-if="fruta.stock > 10">
        Nombre: {{ fruta.name }} <br>
        Precio: {{ fruta.price }} <br>
        Descripción: {{ fruta.descripcion }} <br>
        Stock: {{ fruta.stock }}
      </li>
    </template>
  </ul>
  <ul>
    <li v-for="value, propiedad in objetoFruta" :key="value">
      {{ propiedad }} : {{ value }}
    </li>
  </ul>
  <button @click.right.prevent="hacerClick">Presionar boton</button>
  <div class="container text-center mt-2">
    <h1 :class="classCounter">{{ counter }}</h1>
    <div class="btn-group">
      <button @click="aumentarContador" class="btn btn-success">Incrementar</button>
      <button @click="disminuirContador" class="btn btn-danger">Decrementar</button>
      <button @click="resetearContador" class="btn btn-secondary">Resetear</button>
      <button :disabled="bloquearBtnAdd" @click="add" class="btn btn-warning">Agregar</button>
    </div>
    <ul class="list-group">
      <li class="list-group-item" v-for="(num,index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>


<style>
h1 {
  color: red;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: white;
}
</style>