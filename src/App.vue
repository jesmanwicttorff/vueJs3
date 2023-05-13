<script setup>
import {ref, computed} from 'vue'
const handleButton = (ms) =>{
console.log("Boton recibido " + ms);
}
let counter = ref(0);
// Definimos ref para que el counter sea reactivo , 
// al ser reactivo nos devuelve un objeto value
const increment =()=>{
  counter.value ++;
  console.log(counter)
  console.log('Incrementar')
}
const classCounter = computed(() =>{
  if(counter.value === 0){
    return 'zero';
  }
  if(counter.value > 0){
    return 'positivo';
  }
  if(counter.value < 0){
    return 'negativo';
  }
})

const ArrayNum = ref([]) // Declaramos un Array Reactivo
const decrement =() =>{counter.value --;}
const reset =() => {counter.value = 0;}
const InsertarArray =() =>{ ArrayNum.value.push(counter.value)}
const bloquearButton = computed (()=>{
 const buscar =  ArrayNum.value.find((num) => num === counter.value)
 console.log(buscar)
 // si existe el numero retorna true para bloquear
  if(buscar == 0) return true
 return buscar ? true : false

 // return buscar || buscar === 0
})
const activo = false
const name = "Jesman Developer"
const color="color:yellow"
const arrayColores = ['Yellow', 'Blue', 'Caracas']
const state = true
const estado = null
const show = false


const ArrayFrutas= ["Mango", "Aguacate", "Lechoza", "Naranja", "Limon"]
const arrayFrutasElem = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock: 10
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 60
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock : 40
        },
    ];
    const objectoFruta = {
            name: "Fresa",
            price: "$7.00",
            description: "Una Fresa",
        }
</script>
<template>
  <div class="container text-center mt-3">
  <h1>Hola Vue3 {{ name.toUpperCase() }}</h1><br>
  <h2 :style="color">Bienvenido {{ arrayColores }}</h2><br/>
  <h2 :style="`color:${arrayColores[1]}`">Soy de Caracas</h2><br/>
  <h2 v-if="estado == true"> {{ "Estoy trabajando" }}</h2>
  <h2 v-else-if="activo == false">{{ "No estoy Trabajando" }}</h2>
  <h2 v-else>{{ "Estoy Jugando Play Station" }}</h2><br/>
  <p v-show="show"> Estoy en Curso Vue3</p><br/>
  <div class="btn.group">
  <button v-on:click.right.prevent="handleButton('texto Right')">Activame Right</button><br/>
  <button v-on:click="handleButton('texto left')">Activame Left</button><br/>
  <button v-on:click.middle="handleButton('texto Medio')">Activame Medio</button><br/>
<!----  <p :class="counter >0 ? 'positivo' : 'negativo'">{{ counter }}</p><br/>  -->
  <p :class="classCounter">{{ counter }}</p><br/>
  <button @click="increment" class="btn btn-success">Incrementar</button>
  <button @click="decrement" class="btn btn-danger">Decrementar</button>
  <button @click="reset" class="btn btn-secondary">Reset</button>
  <button class="btn btn-primary" :disabled="bloquearButton" @click="InsertarArray">Agregar a la Lista</button><br/>
</div>
  <br/>
  <br/>
  <!-- Agregamos la lista-->
 <!--- <ul>
    <li>
     {{ ArrayNum }}
    </li>
  </ul><br/> -->
  <ul class="list-group mt-3"> 
    <li class="list-group-item" v-for="(num,index) in ArrayNum"
    :key="index">
   {{ num }}
    </li>
  </ul>
  
  
  <h2> 
    {{ state ?  "Estoy activo"  :  "Estoy Inactivo" }}
  </h2><br/>
  <!----
  <ul>
  <li v-for ="(fruta,index) in ArrayFrutas"
      :key="index">
        {{ index }} - {{ fruta }}
  </li>
</ul><br/>
-->
<ul>
  <template v-for="(fruit,index) in arrayFrutasElem"
  :key="index">
   <li v-if="fruit.stock >20">
       {{index }} - {{ fruit.name }} - {{ fruit.description }} - {{ fruit.price }}
   </li>
   </template>
</ul><br/>
<!----
<ul>
  <li v-for="(value,propiedad, index) in objectoFruta" :key="value">
 {{ index }} - {{ propiedad }} : {{ value }}
  </li>
</ul>
-->
</div>
</template>
<style>
h1 {
color:red;
}
.positivo {
  color: green;
}
.negativo {
  color: red;
}
.zero {
  color: peru;
}
</style>