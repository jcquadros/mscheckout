<template>
  <div v-if="!loading">
    <q-list>
      <q-item v-ripple v-for="(item, index) in products" :key="index" dense>
        <q-item-section>
          <q-item-label>{{ item.name }}</q-item-label>
          <q-item-label caption>{{ item.price }}</q-item-label>
        </q-item-section>
        <q-item-section avatar>
          <q-avatar rounded>
            <img :src="item.image" />
          </q-avatar>
        </q-item-section>
      </q-item>

      <q-separator />
      <q-item>
        <q-item-section>
          <q-item-label>Data de Compra:</q-item-label>
          <q-item-label caption>{{ purchaseDate }}</q-item-label>
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label>Previsão de Entrega:</q-item-label>
          <q-item-label caption>{{ deliveryDate }}</q-item-label>
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label>Método de Pagamento:</q-item-label>
          <q-item-label caption>{{ paymentMethod }}</q-item-label>
        </q-item-section>
      </q-item>

      <q-item>
        <q-item-section>
          <q-item-label>Valor Total:</q-item-label>
          <q-item-label caption>{{ totalPrice }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </div>
  <div v-else class="flex flex-center q-pa-md">
    <div class="text-center">
      <div>Carregando...</div>
      <q-circular-progress
        indeterminate
        rounded
        size="50px"
        color="primary"
        class="q-ma-md"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import productsData from 'src/assets/products.json';

const loading = ref(true);
const products = ref(productsData.products);
const purchaseDate = ref('May 13, 2024');
const deliveryDate = ref('May 20, 2024');
const paymentMethod = ref('Cartão de Crédito');
const totalPrice = computed(() => {
  return products.value.reduce((acc, product) => acc + product.price, 0);
});

setTimeout(() => {
  loading.value = false;
}, 1000);
</script>
