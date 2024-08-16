<template>
<h2>
    Cena {{ contador + 1 }}
    con el Rey godo {{ rey }}
</h2>
<h3 class="precio">Precio: {{ preciRey }}$</h3>
<br>
<img :src="imagen" alt="">
<br>
<button @:click="siguiente">Siguiente ({{contador + 1}} / {{total}})</button>
</template>

<script setup>
import { ref, computed } from 'vue';
import {productos} from './data.js'

// Cantidad de datos
const contador = ref(0)
const total = productos.length

// Botones
const siguiente = () => {
    contador.value ++
    if(contador.value >= total){
        contador.value = 0
    }
}

// Elementos
const rey = computed(() => {
    const nombreRey = productos[contador.value].nombre.toLowerCase()
    return nombreRey.substring(0,1).toUpperCase() + nombreRey.substring(1)
})

const preciRey = computed(() => {
    return productos[contador.value].precio
})

// Imagenes
const ruta = "https://www.html6.es/img/rey_"

const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})
</script>

<style scoped>

</style>