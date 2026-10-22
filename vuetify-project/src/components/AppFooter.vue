
<script setup>
import { computed } from 'vue'

defineProps({
  nombre: {
    type: String,
    default: 'Roberto Reyna',
  },
  matricula: {
    type: String,
    default: '1155428',
  },
  contacto: {
    type: String,
    default: 'roberto.reyna@uabc.edu.mx',
  },
})

const fechaActual = computed(() =>
  new Intl.DateTimeFormat('es-MX', {
    dateStyle: 'long',
  }).format(new Date()),
)
</script>


<template>
  <v-footer color="primary" class="py-1">
    <v-container class="py-0">
      <v-row align="center" dense>
        <v-col cols="12" md="6" class="py-1">
          <div class="text-body-2 font-weight-bold">
            {{ nombre }}
          </div>
          <div class="text-caption">Matrícula: {{ matricula }}</div>
        </v-col>

        <v-col cols="12" md="6" class="py-1 text-md-end">
          <div v-if="contacto" class="text-caption">
            Contacto: {{ contacto }}
          </div>
          <div class="text-caption">
            © {{ new Date().getFullYear() }} — {{ nombre }}
          </div>
          <div class="text-caption">Fecha: {{ fechaActual }}</div>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>
