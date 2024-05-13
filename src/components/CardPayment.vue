<template>
  <div class="flex flex-center">
    <div v-if="loading" class="text-center">
      <div>Validando seu cartão...</div>
      <q-circular-progress
        indeterminate
        rounded
        size="50px"
        color="primary"
        class="q-ma-md"
      />
    </div>
    <div v-else class="text-center">
      <div>Compra finalizada.</div>
      <q-icon name="check_circle" size="50px" color="green" class="q-ma-md" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const loading = ref(true);

setTimeout(() => {
  loading.value = false;
}, 2000);
</script>
