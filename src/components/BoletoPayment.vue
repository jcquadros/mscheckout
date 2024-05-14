<template>
  <div class="q-pa-md">Pagamento com boleto</div>
  <embed
    class="q-pa-md"
    :src="boleto"
    type="application/pdf"
    width="100%"
    height="600px"
  />
</template>

<script setup lang="ts">
import boletoPDF from '../assets/boleto.pdf';
import { ref } from 'vue';

const boleto = ref(boletoPDF);
</script>
