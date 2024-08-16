<template>
<h2>
    Cena {{ contador + 1 }}
    con el Rey godo {{ rey }}
</h2>
<h3 class="precio">Precio: {{ precioRey }}$</h3>
<div v-if="disponible" class="dias soloFinesDeSemana">(Sólo fines de semana)</div>
<div v-else class="dias todosLosDias">(De lunes a domingo)</div>
<div v-if="precioRey < 100" class="oferta">
    <div>
        Ahora un 10% de descuento
        {{ nuevoPrecio }}$
    </div>
    <img src="/oferta.jpg" alt="Rey godo en descuento">
</div>
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

const precioRey = computed(() => {
    return productos[contador.value].precio
})

const disponible = computed(() => {
    return productos[contador.value].finDeSemana
})

const nuevoPrecio = computed(() => {
    return Number(productos[contador.value].precio / 1.10).toFixed(2)
})

// Imagenes
const ruta = "https://www.html6.es/img/rey_"

const imagen = computed(() => {
    return `${ruta}${productos[contador.value].nombre.toLowerCase()}.png`
})
</script>

<style scoped>
.todosLosDias {
    background-color: green;
}

.soloFinesDeSemana {
    background-color: red;
}
</style>