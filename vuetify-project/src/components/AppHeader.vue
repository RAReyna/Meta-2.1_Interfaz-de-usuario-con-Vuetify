
<script setup>
defineProps({
  titulo: {
    type: String,
    default: 'Mi portafolio fotográfico',
  },
  subtitulo: {
    type: String,
    default: 'Una colección de fotografías',
  },
  imagenPerfil: {
    type: String,
    default: 'https://picsum.photos/id/64/100/100',
  },
})
</script>

<template>
  <v-app-bar color="primary" elevation="2">
    <v-container class="d-flex align-center">
      <v-avatar size="44" class="mr-3">
        <v-img
          :src="imagenPerfil"
          alt="Imagen de perfil"
          cover
        />
      </v-avatar>

      <div class="text-truncate">
        <v-app-bar-title class="pa-0">
          {{ titulo }}
        </v-app-bar-title>

        <div class="text-caption text-truncate">
          {{ subtitulo }}
        </div>
      </div>
    </v-container>
  </v-app-bar>
</template>
