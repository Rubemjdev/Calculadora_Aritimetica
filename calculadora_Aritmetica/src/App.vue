<script setup>
  import 'bootstrap/dist/css/bootstrap.min.css'

</script>

<template>
  <div class="container">
    <header class="text-center mt-3 mb-3 bg-light p-3 rounded-5">
      <h1>Olá</h1>
      <p>
        Selecione o tipo da operação e digite os números a serem calculados
      </p>
    </header>
    <div class="card p-4 shadow-sm">
      <div class="row">
        <div class="col-md-4 mb-3">
          <label for="numero1" class="form-label">Número 1</label>
          <input type="number" id="numero1" class="form-control" placeholder="Digite o primeiro número">
        </div>

        <div class="col-md-4 mb-3">
          <label for="numero2" class="form-label">Número 2</label>
          <input type="number" id="numero2" class="form-control" placeholder="Digite o segundo número">
        </div>

        <div class="col-md-4 mb-3">
          <label for="resposta" class="form-label">Resposta</label>
          <input type="number" id="resposta" class="form-control" readonly placeholder="Seu resultado é: ">
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
