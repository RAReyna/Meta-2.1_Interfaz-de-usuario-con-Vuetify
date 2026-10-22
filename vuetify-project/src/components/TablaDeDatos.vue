```vue
<script setup>
import { ref } from 'vue'

const habilidades = ref([
  {
    name: 'Python',
    nivelDominio: 'Intermedio',
    exp: 2,
  },
  {
    name: 'JavaScript',
    nivelDominio: 'Principiante',
    exp: 0,
  },
  {
    name: 'C',
    nivelDominio: 'Intermedio',
    exp: 4,
  },
  {
    name: 'Java',
    nivelDominio: 'Intermedio',
    exp: 4,
  },
])
</script>

<template>
  <v-table>
    <thead>
      <tr>
        <th class="text-left">Habilidades</th>
        <th class="text-left">Nivel de dominio</th>
        <th class="text-left">Años de experiencia</th>
      </tr>
    </thead>

    <tbody>
      <tr
        v-for="item in habilidades"
        :key="item.name"
      >
        <td>{{ item.name }}</td>
        <td>{{ item.nivelDominio }}</td>
        <td>{{ item.exp }}</td>
      </tr>
    </tbody>
  </v-table>
</template>
``` 