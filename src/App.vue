<script setup>
import {ref, computed} from 'vue';
const name = "Vue 3";

const counter = ref(0)

let listaNumerosFavoritos = ref([])
const deshabilitado = ref(false) 

//metodo - methods
const incrementar = () => {counter.value ++;}


const disminuir = () => {counter.value --;}


const resetear = () => {
  counter.value = 0
  listaNumerosFavoritos.value = []
}

const classCounter = computed(() => {
  if(counter.value === 0){
    return 'zero'
  }

  if(counter.value > 0){
    return 'positivo'
  }

  if(counter.value < 0){
    return 'negativo'
  }
})

const agregar = () =>{ listaNumerosFavoritos.value.push(counter.value)}
const habilitar = computed(()=>{
  let encontrado = listaNumerosFavoritos.value.find((num) => num === counter.value )
  if(encontrado === 0) return true
  return encontrado ? true : false
  //return encontrado || encontrado === 0
})

</script>

<template>
  <div class="container text-center mt-3">
    <h2 :class="classCounter"> 
      {{ counter }}
    </h2>
    <div class="btn-group">
      <button @click="incrementar" class="btn btn-success">Aumentar</button>
      <button @click="disminuir" class="btn btn-danger">Disminuir</button>    
      <button @click="resetear" class="btn btn-secondary">Resetear</button>
      <button @click="agregar" :disabled="habilitar" class="btn btn-primary">Agregar</button>
    </div>
    <ul class="list-group list-group-flush">
      <li
        v-for="(numero, key) in listaNumerosFavoritos"
        :key="key"
        class="list-group-item"
      >{{ numero }}</li>
    </ul>
  </div>
  
</template>

<style>
  h1{
    color:blueviolet
  }

  .positivo {
    color: green;
  }

  .negativo{
    color: red;
  }

  .zero{
    color: orange;
  }
</style>