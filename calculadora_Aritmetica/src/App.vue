<script setup>
  import 'bootstrap/dist/css/bootstrap.min.css'
  import { computed, onMounted, onUnmounted, reactive, ref } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Body from './components/Body.vue';

const estado = reactive({
  numero1: '',
  numero2: '',
  operacao: 'soma',
})

const tempoRestante = ref(10);
let timerId = null;

const resultado = computed(() => {
  const { numero1, numero2, operacao } = estado;

  switch (operacao) {
    case 'soma':
      return numero1 + numero2;
    case 'sub':
      return numero1 - numero2;
    case 'multi':
      return numero1 * numero2;
    case 'divi':
      return numero1 / numero2;
    default:
      return 0;
  }
});

const zerarCampos = () => {
  estado.numero1 = '';
  estado.numero2 = '';
  estado.operacao = 'soma';
}

const iniciarTemporizador = () => {
  if(timerId) {
    clearInterval(timerId);
  }
  tempoRestante.value = 10;
  timerId = setInterval(() => {
    tempoRestante.value--;

    if(tempoRestante.value <=0) {
      zerarCampos();
      clearInterval(timerId);
    }
  }, 1000);
}

const reiniciarTemporizador = () => {
  iniciarTemporizador();
}

onMounted(() => {
  iniciarTemporizador();
});

onUnmounted(() => {
  if(timerId) {
    clearInterval(timerId);
  }
});

</script>

<template>
  <div class="container">
    <Cabecalho />
    <Body :estado="estado" :resultado="resultado" :reiniciar-temporizador="reiniciarTemporizador" :tempo-restante="tempoRestante" />
    
  </div>
</template>

<style scoped>

</style>
