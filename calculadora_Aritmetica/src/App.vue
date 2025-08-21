<script setup>
import 'bootstrap/dist/css/bootstrap.min.css'
import { computed, onMounted, onUnmounted, reactive, ref } from 'vue';

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
    <header class="text-center mt-3 mb-3 bg-light p-3 rounded-5 shadow-sm">
      <h1>Olá</h1>
      <p>
        Selecione o tipo da operação e digite os números a serem calculados
      </p>
    </header>
    <div class="card p-4 shadow-lg">
      <div class="card-body">
        <div class="row">
          <div class="col-md-4 mb-4">
            <label class="form-label" for="operacao">
              Selecione a Operação:
            </label>
            <select id="operacao" class="form-select" @change="reiniciarTemporizador" v-model="estado.operacao">
              <option value="soma">Soma</option>
              <option value="sub">Subtração</option>
              <option value="multi">Multiplicação</option>
              <option value="divi">Divisão</option>
            </select>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-4 mb-3">
          <label for="numero1" class="form-label">Número 1</label>
          <input type="number" @input="reiniciarTemporizador" id="numero1" v-model.number="estado.numero1" class="form-control" placeholder="Digite o primeiro número">
        </div>
        <div class="col-md-4 mb-3">
          <label for="numero2" class="form-label">Número 2</label>
          <input type="number" id="numero2" @input="reiniciarTemporizador" v-model.number="estado.numero2" class="form-control" placeholder="Digite o segundo número">
        </div>

        <div class="col-md-4 mb-3">
          <label for="resposta" class="form-label">Resposta</label>
          <input type="number" id="resposta" :value="resultado" class="form-control" readonly placeholder="Seu resultado é: ">
        </div>
      </div>
      <div class="temporizador text-center mt-4">
        <p>Tempo Restante</p>
        <span class="badge bg-danger">{{ tempoRestante }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
