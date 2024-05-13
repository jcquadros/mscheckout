<template>
  <div class="q-pa-md">
    <q-stepper
      v-model="step"
      ref="stepper"
      color="primary"
      animated
      @before-transition="manipulaPassos"
    >
      <q-step
        :name="1"
        title="Selecione um método de pagamento"
        icon="settings"
        :done="step > 1"
      >
        <div class="q-gutter-sm">
          <q-radio v-model="shape" :val="BoletoForm" label="boleto" />
          <q-radio
            v-model="shape"
            :val="CreditCardForm"
            label="cartão de crédito"
          />
          <q-radio v-model="shape" :val="PixPayment" label="pix" />
        </div>
      </q-step>

      <q-step
        :name="2"
        title="Preencha o formulário"
        caption="Optional"
        icon="assignment"
        :done="step > 2"
      >
        <component :is="shape" @submit="validateForm"></component>
      </q-step>

      <q-step :name="3" title="Pagamento" icon="paid" :done="step > 3">
        <component :is="payment" :formulario="formulario" />
      </q-step>

      <q-step :name="4" title="Resumo da Compra" icon="shopping_cart">
        <SummaryBuy></SummaryBuy>
      </q-step>

      <template v-slot:navigation>
        <q-stepper-navigation>
          <q-btn
            @click="stepper?.next()"
            color="primary"
            :label="step === 4 ? 'Finish' : 'Continue'"
            :disabled="step === 2 && !isFormValid"
          />
          <q-btn
            v-if="step > 1"
            flat
            color="primary"
            @click="stepper?.previous()"
            label="Back"
            class="q-ml-sm"
          />
        </q-stepper-navigation>
      </template>
    </q-stepper>
  </div>
</template>

<script setup lang="ts">
import { computed, ref, shallowRef } from 'vue';
import { QStepper } from 'quasar';
import BoletoForm from 'src/components/BoletoForm.vue';
import CreditCardForm from 'src/components/CreditCardForm.vue';
import PixPayment from 'src/components/PixPayment.vue';
import CardPayment from 'src/components/CardPayment.vue';
import BoletoPayment from 'src/components/BoletoPayment.vue';
import SummaryBuy from 'src/components/SummaryBuy.vue';

const step = ref(1);
const stepper = ref(<QStepper | null>null);
const shape = shallowRef(BoletoForm);
const isFormValid = ref(false);
const formulario = ref({});

const payment = computed(() => {
  if (shape.value === BoletoForm) {
    return BoletoPayment;
  } else if (shape.value === CreditCardForm) {
    return CardPayment;
  } else if (shape.value === PixPayment) {
    return PixPayment;
  }
  return null;
});

defineOptions({
  name: 'IndexPage',
});

const validateForm = (formData: [boolean, object]) => {
  isFormValid.value = formData[0];
  formulario.value = formData[1];
};

function manipulaPassos(newStep: string | number, oldStep: string | number) {
  if (shape.value === PixPayment && newStep === 2) {
    if (oldStep === 1) {
      step.value = 3;
    } else if (oldStep === 3) {
      step.value = 1;
    }
  }
}
</script>
