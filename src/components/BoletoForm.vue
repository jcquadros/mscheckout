<template>
  <div>Boleto</div>
  <q-form ref="form">
    <q-input
      v-model="formData.name"
      label="Nome"
      :rules="[
        (val) => !!val || 'Por favor, preencha o nome',
        (val) =>
          (val && val.length <= 50) ||
          'O nome deve ter no máximo 50 caracteres',
      ]"
    ></q-input>
    <q-input
      v-model="formData.lastName"
      label="Sobrenome"
      :rules="[
        (val) => !!val || 'Por favor, preencha o sobrenome',
        (val) =>
          (val && val.length <= 50) ||
          'O sobrenome deve ter no máximo 50 caracteres',
      ]"
    ></q-input>
    <q-input
      v-model="formData.email"
      label="Email"
      type="email"
      :rules="[
        (val) => !!val || 'Por favor, preencha o email',
        (val) => /.+@.+\..+/.test(val) || 'Por favor, insira um email válido',
      ]"
    ></q-input>
    <q-input
      v-model="formData.identification"
      label="Identificação"
      :rules="[
        (val) => !!val || 'Por favor, preencha a identificação',
        (val) =>
          (val && val.length <= 10) ||
          'A identificação deve ter no máximo 10 caracteres',
      ]"
    ></q-input>
  </q-form>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { QForm } from 'quasar';

const formData = ref({
  name: '',
  lastName: '',
  email: '',
  identification: '',
});

const form = ref<QForm | null>(null);
const emit = defineEmits(['submit']);

watch(formData.value, async () => {
  if (form.value && Object.values(formData.value).every((value) => !!value)) {
    const isValid = await form.value?.validate(false);
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
