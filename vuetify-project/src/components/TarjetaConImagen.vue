
<script setup>
import { computed } from 'vue'

const props = defineProps({
  imagen: {
    type: String,
    required: true,
    validator: (value) => value.startsWith('https://'),
  },
  titulo: {
    type: String,
    required: true,
  },
  descripcion: {
    type: String,
    required: true,
  },
  autor: {
    type: String,
    required: true,
  },
})

const imagenValida = computed(() => props.imagen)
</script>

<template>
  <v-card class="h-100" elevation="3">
    <v-img
      :src="imagenValida"
      height="200"
      cover
      :alt="`Fotografía de ${autor}`"
    />

    <v-card-title>{{ titulo }}</v-card-title>

    <v-card-subtitle>
      Fotografía por {{ autor }}
    </v-card-subtitle>

    <v-card-text>
      {{ descripcion }}
    </v-card-text>
  </v-card>
</template>
