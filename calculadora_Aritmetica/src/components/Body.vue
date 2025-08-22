<script setup>
    const props = defineProps(['reiniciarTemporizador', 'tempoRestante',
        'estado', 'resultado']);
</script>

<template>
    <div class="card p-4 shadow-lg">
        <div class="card-body">
            <div class="row">
                <div class="col-md-4 mb-4">
                    <label class="form-label" for="operacao">
                        Selecione a Operação:
                    </label>
                    <select id="operacao" class="form-select" @change="props.reiniciarTemporizador" v-model="props.estado.operacao">
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
                <input type="number" @input="props.reiniciarTemporizador" id="numero1" v-model.number="props.estado.numero1"
                    class="form-control" placeholder="Digite o primeiro número">
            </div>
            <div class="col-md-4 mb-3">
                <label for="numero2" class="form-label">Número 2</label>
                <input type="number" id="numero2" @input="props.reiniciarTemporizador" v-model.number="props.estado.numero2"
                    class="form-control" placeholder="Digite o segundo número">
            </div>

            <div class="col-md-4 mb-3">
                <label for="resposta" class="form-label">Resposta</label>
                <input type="number" id="resposta" :value="props.resultado" class="form-control" readonly
                    placeholder="Seu resultado é: ">
            </div>
        </div>
        <div class="temporizador text-center mt-4">
            <p>Tempo Restante</p>
            <span class="badge bg-danger">{{ props.tempoRestante }}</span>
        </div>
    </div>
</template>