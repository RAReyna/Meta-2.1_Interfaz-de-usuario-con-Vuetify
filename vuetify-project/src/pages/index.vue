```vue
<script setup>
import { ref, onMounted } from 'vue'
import TarjetaConImagen from '@/components/TarjetaConImagen.vue'
import TablaDeDatos from '@/components/TablaDeDatos.vue'

const imagenes = ref([
  {
    id: '10',
    imagen: 'https://picsum.photos/id/10/600/400',
    autor: 'Cargando...',
  },
  {
    id: '20',
    imagen: 'https://picsum.photos/id/20/600/400',
    autor: 'Cargando...',
  },
])

const cargando = ref(false)
const error = ref('')

async function actualizarImagenes() {
  cargando.value = true
  error.value = ''

  try {
    const respuesta = await fetch(
      'https://picsum.photos/v2/list?page=1&limit=50',
    )

    if (!respuesta.ok) {
      throw new Error('No se pudieron obtener las imágenes.')
    }

    const datos = await respuesta.json()

    if (datos.length < 2) {
      throw new Error('La API no devolvió suficientes imágenes.')
    }

    // Elegir dos imágenes diferentes de la respuesta.
    const seleccionadas = []

    while (seleccionadas.length < 2) {
      const indice = Math.floor(Math.random() * datos.length)
      const candidata = datos[indice]

      if (!seleccionadas.some((imagen) => imagen.id === candidata.id)) {
        seleccionadas.push(candidata)
      }
    }

    // Actualizar las dos tarjetas con los datos de Picsum.
    imagenes.value = seleccionadas.map((imagen) => ({
      id: imagen.id,
      imagen: `https://picsum.photos/id/${imagen.id}/600/400`,
      autor: imagen.author,
    }))
  } catch (err) {
    error.value =
      'No fue posible cargar las fotografías. Comprueba tu conexión e inténtalo de nuevo.'
    console.error(err)
  } finally {
    cargando.value = false
  }
}

onMounted(actualizarImagenes)
</script>

<template>
  <v-container class="py-8">
    <h1 class="text-h4 mb-6">Mi portafolio fotográfico</h1>

    <v-row>
      <v-col
        v-for="(imagen, indice) in imagenes"
        :key="imagen.id"
        cols="12"
        md="6"
      >
        <TarjetaConImagen
          :imagen="imagen.imagen"
          :titulo="`Fotografía ${indice + 1}`"
          descripcion="Fotografía seleccionada de la colección de Picsum."
          :autor="imagen.autor"
        />
      </v-col>
    </v-row>

    <div class="d-flex justify-center my-6">
      <v-btn
        color="primary"
        prepend-icon="mdi-refresh"
        :loading="cargando"
        :disabled="cargando"
        @click="actualizarImagenes"
      >
        Actualizar fotografías
      </v-btn>
    </div>

    <v-alert
      v-if="error"
      type="error"
      variant="tonal"
      closable
      class="mb-6"
      @click:close="error = ''"
    >
      {{ error }}
    </v-alert>

    <TablaDeDatos />
  </v-container>
</template>
```