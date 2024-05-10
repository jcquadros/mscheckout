<template>
  <div>Cartão</div>
  <q-form ref="form">
    <q-select
      dense
      filled
      v-model="formData.bandeira"
      :options="bandeiraOptions"
      label="Bandeira"
      :rules="[(val) => !!val || 'Por favor, selecione uma bandeira']"
    >
      <template v-slot:option="scope">
        <q-item v-bind="scope.itemProps">
          <q-item-section avatar>
            <q-icon :name="scope.opt.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ scope.opt.label }}</q-item-label>
          </q-item-section>
        </q-item>
      </template>
    </q-select>

    <q-input
      dense
      v-model="formData.cardNumber"
      label="Número do Cartão"
      :rules="[
        (val) => !!val || 'Por favor, preencha o número do cartão',
        (val) =>
          (val && /^\d{16}$/.test(val)) ||
          'O número do cartão deve conter 16 dígitos',
      ]"
    ></q-input>

    <q-input
      dense
      v-model="formData.cvv"
      label="CVV"
      :rules="[
        (val) => !!val || 'Por favor, preencha o CVV',
        (val) => (val && /^\d{3}$/.test(val)) || 'O CVV deve conter 3 dígitos',
      ]"
    ></q-input>

    <q-input
      dense
      v-model="formData.expirationDate"
      label="Data de Expiração"
      :rules="[
        (val) => !!val || 'Por favor, preencha a data de expiração',
        (val) =>
          (val && /^\d{2}\/\d{2}$/.test(val)) ||
          'A data de expiração deve estar no formato MM/AA',
      ]"
    ></q-input>

    <q-input
      dense
      v-model="formData.titular"
      label="Titular"
      :rules="[(val) => !!val || 'Por favor, preencha o titular']"
    ></q-input>

    <q-input
      dense
      v-model="formData.cpf"
      label="CPF"
      :rules="[
        (val) => !!val || 'Por favor, preencha o CPF',
        (val) =>
          (val && /^\d{3}\.\d{3}\.\d{3}-\d{2}$/.test(val)) ||
          'O CPF deve estar no formato XXX.XXX.XXX-XX',
      ]"
    ></q-input>

    <q-select
      filled
      dense
      v-model="formData.parcelas"
      :options="parcelasOptions"
      label="Parcelas"
      :rules="[(val) => !!val || 'Por favor, selecione o número de parcelas']"
    ></q-select>
  </q-form>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { QForm } from 'quasar';

const form = ref(<QForm | null>null);
const emit = defineEmits(['submit']);

const formData = ref({
  bandeira: '',
  cardNumber: '',
  cvv: '',
  expirationDate: '',
  titular: '',
  cpf: '',
  parcelas: '',
});

const bandeiraOptions = [
  {
    label: 'Mastercard',
    value: 'Mastercard',
    icon: 'fab fa-cc-mastercard',
  },
  {
    label: 'Visa',
    value: 'Visa',
    icon: 'fab fa-cc-visa',
  },
];

const parcelasOptions = [
  {
    label: '1x',
    value: '1',
  },
  {
    label: '2x',
    value: '2',
  },
  {
    label: '3x',
    value: '3',
  },
  {
    label: '4x',
    value: '4',
  },
  {
    label: '5x',
    value: '5',
  },
  {
    label: '6x',
    value: '6',
  },
];

watch(formData.value, async () => {
  if (form.value && Object.values(formData.value).every((value) => !!value)) {
    const isValid = await form.value?.validate();
    if (isValid) {
      emit('submit', [true, formData.value]);
      console.log('form is valid');
    } else {
      emit('submit', [false, formData.value]);
      console.log('form is invalid');
    }
  }
});
</script>
