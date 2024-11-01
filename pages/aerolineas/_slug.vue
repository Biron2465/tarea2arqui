<template>
  <div v-if="aerolinea">
    <h1>{{ aerolinea.nombre }}</h1>
    <p><strong>País de Origen:</strong> {{ aerolinea.pais_origen }}</p>
    <p><strong>Flota:</strong> {{ aerolinea.flota }}</p>
    <p><strong>Modelos Operados:</strong></p>
    <ul>
      <li v-for="modelo in aerolinea.modelos_operados" :key="modelo">{{ modelo }}</li>
    </ul>
    <Comments /> <!-- Agregar la sección de comentarios -->
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'
import Comments from '@/components/Comments.vue'

const route = useRoute()
const aerolinea = ref(null)

onMounted(async () => {
  // Cargar la información de la aerolínea
  const { nombre } = route.params
  const response = await axios.get('/data/aerolineas.json')
  aerolinea.value = response.data.find(a => a.nombre === nombre)
})
</script>
