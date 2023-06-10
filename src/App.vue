<!--single -->
<script setup>
import { ref, computed } from 'vue';
const saludo = 'mundo cruel';
const fontWeight = '300;';
const arrayColors = ['red', 'green', 'black', 'violet', 'yellow'];
const test = true;
const objectsArrayTest = [
  {
    name: 'apple',
    price: '$2.00',
    decription: 'is red and tastes good',
    stock: 10,
  },
  {
    name: 'pear',
    price: '$2.50',
    decription: 'is green and tastes weird',
    stock: 0,
  },
  {
    name: 'pineapple',
    price: '$4.99',
    decription: 'is yellow and have spikes',
    stock: 20,
  },
  {
    name: 'banana',
    price: '$1.50',
    decription: 'is yellow and tastes delicious',
    stock: 5,
  },
  {
    name: 'watermelon',
    price: '$5.50',
    decription: 'is green and is refreshing',
    stock: 3,
  },
];
const eventClick = () => {
  alert('has pinchado en el btn');
};
const eventClick2 = (message) => alert(message);
// reactiividad
const cont = ref(0);
// computed
const contComputed = ref(0);
const computedClassStyle = computed(() => {
  if (contComputed.value > 0) {
    return 'positive';
  }
  if (contComputed.value < 0) {
    return 'negative';
  }
  if (contComputed.value === 0) {
    return 'zero';
  }
});
// test
const contTest = ref(0);
const arrayTest = ref([]);
const computedTest = computed(() => {
  if (contTest.value > 0) {
    return 'positive';
  }
  if (contTest.value < 0) {
    return 'negative';
  }
  if (contTest.value === 0) {
    return 'zero';
  }
});
const addValue = () => {
  arrayTest.value.push(contTest.value);
};
const computedDisabledTest = computed(() => {
  return arrayTest.value.includes(contTest.value) ? true : false;
});
</script>
<!-- file -->
<template>
  <!-- conectar el js con el html ({{ variable }}) y uso de v-bind:style o :style (para dar estilo), uso de expresiones de js como los metodos ("."), operadores ternarios (? :) y manejo de arrays  -->
  <h1>hola {{ saludo.toUpperCase() }}</h1>
  <!-- `se puede usar algunos metodos de js con el "." depues de la variable` -->
  <h2 v-bind:style="`font-weight: ${fontWeight}; color: ${arrayColors[0]}`">
    Usando (<b>v-bind:style="estilo css</b>")
  </h2>
  <h2 :style="`font-weight: ${fontWeight}; color: ${arrayColors[0]}`">
    Usando la abreviacion (<b>:style="estilo css</b>")
  </h2>
  <h2 :style="`color: ${arrayColors[1]}`">Array por el index con el v-bind</h2>
  <h2 :style="`font-weight: ${fontWeight}; color: ${arrayColors[2]}`">
    expresiones de js con operadores ternarios:
    <b>{{ test ? 'I`m true' : 'I`m false' }}</b
    ><!--depende de lo qde el condicional terciario (solo se puede con condicionales terciarios)   -->
    <!-- <b>{{ test ? 'I`m true' : 'I`m false' }}</b> se puede copiar y pegar facilmente con ctrl + ... -->
  </h2>

  <!-- Directivas v-if , v-show  (v-if cuando son operaciones de poco uso y v-show cuando quiere estar alternando en aparecer y desaparecer con mucha frecuencia algo)-->

  <!-- v-if, v-else-if, v-else (si quiere hacer una cadena de condicionales deben estar pegador uno del otro) -->
  <h2 v-if="test === true">Estoy activo</h2>
  <!-- si el condicional (test) es true aparece en caso contrario se comenta y apareceria el de abajo -->
  <h2 v-else-if="test === false">Estoy inactivo</h2>
  <!-- este apareceria si el condicional (test) es false en caso contrario se comenta y apareceria el de arriba --->
  <h2 v-else>Estoy indeciso</h2>
  <!-- si ninguno de los if o else-if se cumple se cumpliria el else -->

  <h2 v-show="test">Estoy on</h2>
  <!-- si es el condicional (test) es true aparece en caso contario se coloca un display:"none" -->
  <h2 v-show="!test">Estoy off</h2>
  <!-- si es el condicional (test) es false aparece en caso contario se coloca un display:"none" -->

  <!-- v-for (parecido al for of/for in) -->
  <ul :style="`list-style: none; padding: 0 0 0 10px;`">
    <li v-for="(element, index) in arrayColors" :key="index">
      {{ index }} - {{ element }}
    </li>
    <!-- aqui el me esta creando los li con cada elemento del array, el primer argumento es el nombre del elemento, el segundo es el index del elemento luego in y ya va el array o objeto (en vue los objetos y loss array se pueden iterar con in o of no importa cual) a iterar, luego :key (q seria como un v-bind:key) seria una ayuda para q vue pueda identificar los elementos a iterar q tiene q ser algo q no se repita como el index  -->
  </ul>
  <h1 :style="`font-size: 40px`">Prueba</h1>
  <ul :style="`border: 2px solid black; background-color: #0fff00`">
    <h1>v-for en un array</h1>
    <li v-for="element in objectsArrayTest" :key="element.name">
      <div>
        <h3>Name: {{ element.name.toUpperCase() }}</h3>
        <p>
          Price: <b>{{ element.price }}</b>
          <span :style="`display: block`"
            >Description: {{ element.decription }}</span
          >
        </p>
      </div>
    </li>
  </ul>
  <!-- v-for pero con solo objetos -->
  <ul :style="`border: 2px solid black; background-color: #f00`">
    <h1>v-for en un objeto</h1>
    <li
      :style="`font-size: 22px`"
      v-for="(value, key, index) in objectsArrayTest[0]"
      :key="value"
    >
      <!-- en los objetos con el v-for q es un for in o un for of se el pasan 2 parametros en valor y la clave y uno opcional q es el index y luego ya se trabaja con ellos -->
      {{ index }}-{{ key }}: {{ value }}
    </li>
  </ul>

  <!-- usando v-if con v-for -->
  <ul :style="`border: 2px solid black; background-color: #0f00ff`">
    <h1>v-for con v-if usando template</h1>
    <template v-for="(value, index) in objectsArrayTest" :key="index">
      <!-- Toca usar el v-for en un template para q despues el v-if pueda filtrar los elementos capturados ya q el v-if tiene mas poder sobre v-for y se lee primero entonces si se hacen en la misma linea siempre se va aleer primero el v-if por ende no va a existir el v-for cuando se lea el v-if   -->
      <li v-if="value.stock > 5">
        name: {{ value.name }} - price: {{ value.price }} - stock:
        {{ value.stock }}
      </li>
    </template>
  </ul>

  <!-- manejo de eventos -->
  <!-- se colocan los eventos con v-on:event o con el "@" antes del nombre del evento -->
  <h2>Usando eventos</h2>
  <button v-on:click="eventClick" name="pinchame xd">Pinchame xd</button>
  <!-- si es sin pararmetro se peude colocar la funcion sin () -->
  <button @click="eventClick2('diste click con el btn izquierdo')">
    click izquierdo
  </button>
  <!-- con parametro si toca colocar los () obviamente -->

  <!-- podemos colocar modificadores a los eventos y tambien los podesmos concatenar (@click.right.prevent), para saber mas sobre los eventos y modificadores de vue.js ingresar a ("https://vuejs.org/guide/essentials/event-handling.html")  -->
  <h2>usando eventos con metodos</h2>
  <button @click.right.prevent="eventClick2('diste click con el btn derecho')">
    click derecho
  </button>
  <button @click.middle="eventClick2('diste click con el btn middle')">
    <!--  -->
    click middle
  </button>

  <!-- reactividad -->
  <h2>Usando variables reactivas</h2>
  <div :style="`margin-top: 10px; display: flex; gap: 20px`">
    <!-- ya con la variable const reactiva por el ref() podemos agregar eventos y se va a ir actualizando el DOM (h2 en este caso) -->
    <button @click="() => cont--">Decrement</button>
    <h3 :class="cont > 0 ? 'positive' : null || cont < 0 ? 'negative' : null">
      {{ cont }}
    </h3>
    <button @click="() => cont++">Increment</button>
    <button @click="() => (cont = 0)">Reset</button>
  </div>
  <h2>Usando Computed con reactividad</h2>
  <div :style="`margin-top: 10px; display: flex; gap: 20px`">
    <button @click="() => contComputed--">Decrement</button>
    <!-- aqui en la calse dinamica colocamos la variable q tenga computed -->
    <h3 :class="computedClassStyle">
      {{ contComputed }}
    </h3>
    <button @click="() => contComputed++">Increment</button>
    <button @click="() => (contComputed = 0)">Reset</button>
  </div>
  <h2 :style="`margin-top: 50px`">Prueba</h2>
  <div
    :style="`margin-top: 10px; display: flex; gap: 20px; background-color: lightblue; padding: 20px; align-items: center; justify-content: center; flex-wrap: wrap`"
  >
    <button class="btn-test btn-test--decrement" @click="() => contTest--">
      Decrement
    </button>
    <!-- aqui en la calse dinamica colocamos la variable q tenga computed -->
    <h3 :class="computedTest">
      {{ contTest }}
    </h3>
    <button class="btn-test btn-test--increment" @click="() => contTest++">
      Increment
    </button>
    <button class="btn-test btn-test--reset" @click="() => (contTest = 0)">
      Reset
    </button>
    <button
      class="btn-test btn-test--add"
      @click="
        () => {
          addValue();
        }
      "
      :disabled="computedDisabledTest"
    >
      Add
    </button>
    <button
      class="btn-test btn-test--watch"
      @click="() => console.log(arrayTest)"
    >
      Watch Changes
    </button>
    <p class="p-test">{{ arrayTest }}</p>
  </div>
</template>
<style scoped>
/* component */
ul {
  list-style: none;
  padding: 0 0 0 20px;
}
h1 {
  color: rgb(51, 6, 6);
}
h1::after {
  content: ':';
}
h2 {
  font-size: 30px;
  background-color: lightsalmon;
}
.negative {
  color: red;
}
.positive {
  color: green;
}
.zero {
  color: #000;
}
.btn-test {
  width: 120px;
  height: 40px;
  border: none;
  border-radius: 12px;
}
.btn-test--increment {
  background-color: lightgreen;
}
.btn-test--decrement {
  background-color: lightcoral;
}
.btn-test--reset {
  background-color: lightyellow;
}
.btn-test--add {
  background-color: lightsalmon;
}
.btn-test--add:disabled {
  background-color: rgb(211, 118, 81);
}
.btn-test--watch {
  background-color: lightpink;
}
.p-test {
  background-color: lightskyblue;
  border-radius: 12px;
  width: 200px;
  min-height: 50px;
  padding: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
