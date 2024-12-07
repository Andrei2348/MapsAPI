<script setup lang="ts">
import MapComponent from '@/components/MapComponent.vue';
</script>

<template>
  <MainLayout>
    <div>
      <h1 class="title">Карта</h1>
      <MapComponent />
    </div>
  </MainLayout>
</template>

<style lang="scss" scoped>
.title {
  color: $blue;
}
</style>
