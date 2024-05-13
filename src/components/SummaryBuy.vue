<template>
  <div class="q-pa-md">
    <div v-if="!loading">
      <q-list>
        <q-item v-ripple v-for="(item, index) in items" :key="index">
          <q-item-section>
            <q-item-label>{{ item.name }}</q-item-label>
            <q-item-label caption>{{ item.price }}</q-item-label>
          </q-item-section>
          <q-item-section avatar>
            <q-avatar rounded>
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
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
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const loading = ref(true);
const items = ref([
  { name: 'Item 1', price: '$10' },
  { name: 'Item 2', price: '$20' },
  { name: 'Item 3', price: '$30' },
]);
const purchaseDate = ref('May 13, 2024');
const deliveryDate = ref('May 20, 2024');
const paymentMethod = ref('Cartão de Crédito');
const totalPrice = ref('$60');

setTimeout(() => {
  loading.value = false;
}, 1000);
</script>
