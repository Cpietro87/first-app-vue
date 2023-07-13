<script setup>
  import { ref } from "vue";
  const name = 'Vue dinamico';
  const styleColor = 'color: blue';
  const arrayColores = ['blue','red','yellow','black', 'peru'];
  const activo = false;
  const arrayFruts = ["🍎", "🍌", "🍉", "🍓", "🍒"];
  const arrayFrutas = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            id: 1,
            stock: 0
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            id: 2,
            stock: 10,
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            id: 3,
            stock: 20,
        },
    ];
  const objetoFruta =  {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            id: 1
        }

  // metodos - method
  const handleClick = (message) =>{
    console.log(message)
  }
  const counter = ref(0);
  const incrementar = () => {
    counter.value++ //se agrega value xq es una variable reactiva 
  }
  const decrementar = () => counter.value --;
  
  const reset = () => (counter.value = 0);
   
</script>

<template>
  <h1>HOla {{ name.toUpperCase()  }}</h1>
  <h2>{{ arrayColores }}</h2>
  <h2 :style="styleColor">Soy azul</h2>
  <h2 :style="`color: ${arrayColores[4]}`">Cambio Colores</h2>
  <h2>{{ activo ? 'activo' : 'inactivo' }}</h2>
  <p v-if="!activo">Esta inactivo</p>
  <p v-show="activo">Estoy Activo v-show</p>
  <h3>recorrer un array</h3>
  <ul>
    <li 
    v-for="(fruta, index) in arrayFruts"
    :key="index"
    >
     {{ index }} - {{ fruta }}
    </li>
  </ul>
  <h3>recorer un array de objetos</h3>
  <ul>
    <li
    v-for="(frutas, name) in arrayFrutas"
    :key="frutas.name">
    {{ frutas.name }} - {{ frutas.price }} - {{ frutas.description }}
    </li>
  </ul>
  <h3>recorrer un objeto</h3>
  {{ objetoFruta }}
  <ul>
    <li 
    v-for="(value, prop, index) in objetoFruta"
    :key="value">
    {{ index }} {{ prop }} : {{ value }}
    </li>
  </ul>
  <h3>v-for con v-if</h3>
  <ul>
    <template v-for="item in arrayFrutas">
      <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }}</li>
    </template>
  </ul>
  <h3>Eventos</h3>
  <button v-on:click="handleClick('Texto 1')"> Activame 1</button>
  <button @click="handleClick('Texto 2')"> Activame 2</button>
  <h3>MOdificadores</h3>
  <button v-on:click.rigth.prevent="handleClick('Texto Right')"> Activame rigth</button>
  <button @click.left="handleClick('Texto Left')"> Activame left</button>
  <button @click.middle="handleClick('Texto Middle')"> Activame middle</button>
  <h3>Variable Reactivas</h3>
  <h4 :class="counter > 0 ? 'positive' : 'negative'">{{ counter }}</h4>
  <button @click="incrementar">Sumar</button>
  <button @click="decrementar">Restar</button>
  <button @click="reset">Reset</button>


</template>

<style>
.positive {
  color: green;
}
.negative {
  color: red;
}
h1 {
  color: red;
  font-weight: bold;
}

</style>