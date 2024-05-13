<template>
  <div class="q-pa-md">
    <div class="column justify-center items-center content-center">
      <div>
        <img
          src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=12191756760"
          alt="QR Code"
        />
      </div>
      <div class="text-center q-ma-md">Escaneie o QR Code para pagar</div>
      <div>
        <q-btn @click="copyToClipboard" label="Copiar código PIX" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useQuasar } from 'quasar';

const q = useQuasar();

const copyToClipboard = () => {
  const pixCode = '1219156760';
  navigator.clipboard
    .writeText(pixCode)
    .then(() => {
      q.dialog({
        title: 'Código PIX copiado!',
        message: 'Agora é só colar no seu app de banco e realizar o pagamento.',
      });
    })
    .catch((error) => {
      q.dialog({
        title: 'Erro ao copiar o código PIX',
        message: error,
      });
    });
};
</script>
