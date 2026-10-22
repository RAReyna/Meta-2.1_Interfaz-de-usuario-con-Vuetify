```vue
<script setup>
import AppHeader from '@/components/AppHeader.vue'
import AppFooter from '@/components/AppFooter.vue'
import IndexPage from '@/pages/index.vue'
</script>

<template>
  <v-app>
    <AppHeader />

    <v-main>
      <IndexPage />
    </v-main>

    <AppFooter />
  </v-app>
</template>
```