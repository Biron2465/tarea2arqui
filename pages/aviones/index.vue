<template>
  <div>
    <Header />
    <div>
      <h1>Lista de Aviones</h1>
      <ul>
        <li v-for="avion in aviones" :key="avion.modelo">
          <nuxt-link :to="{ path: `/aviones/${generateSlug(avion.modelo)}` }">{{ avion.modelo }}</nuxt-link>
        </li>
      </ul>
    </div>
    <Comments /> <!-- Agregar la sección de comentarios -->
    <Footer />
  </div>
</template>

<script setup>
import Header from '@/components/header.vue'
import Footer from '@/components/footer.vue'
import Comments from '@/components/Comments.vue' // Importar Comments
import { ref, onMounted } from 'vue'

const aviones = ref([])

const importAviones = async () => {
  const modules = import.meta.glob('@/data/aviones/*.json')
  const avionPromises = Object.values(modules).map((module) => module())
  const avionData = await Promise.all(avionPromises)
  aviones.value = avionData.map(data => data.default || data)
}

const generateSlug = (text) => {
  return text
    .toString()
    .toLowerCase()
    .replace(/\s+/g, '-')           // Reemplaza espacios con -
    .replace(/[^\w\-]+/g, '')       // Elimina caracteres no válidos
    .replace(/\-\-+/g, '-')         // Reemplaza múltiples - con uno solo
    .replace(/^-+/, '')             // Elimina - al inicio
    .replace(/-+$/, '')             // Elimina - al final
}

onMounted(() => {
  importAviones()
})
</script>

<style scoped>
h1 {
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  text-align: center;
  margin: 0.5rem 0;
}
</style>
