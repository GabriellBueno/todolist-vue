<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import Lista_de_Tarefas from './components/Lista_de_Tarefas.vue';

const estado = reactive({

  filtro: 'todas',
  tarefa_temp: '',

  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para Academia',
      finalizada: true,
    }
  ]
})

const get_tarefas_pendentes = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}

const get_tarefas_finalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const get_tarefas_filtradas = () => {
  const { filtro } = estado

  switch (filtro) {
    case 'pendentes':
      return get_tarefas_pendentes();
    case 'finalizadas':
      return get_tarefas_finalizadas();
    default:
      return estado.tarefas
  }

}

const cadastra_tarefa = () => {
  const tarefa_nova = {
    titulo: estado.tarefa_temp,
    finalizada: false,
  }
  estado.tarefas.push(tarefa_nova);
  estado.tarefa_temp = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas_-pendentes="get_tarefas_pendentes().length"></Cabecalho>
    <Formulario :trocar_filtro="evento => estado.filtro = evento.target.value" :tarefa_-temp="estado.tarefa_Temp" :edita_-tarefa_-temp="evento => estado.tarefa_temp = evento.target.value" :cadastra_-tarefa="cadastra_tarefa"></Formulario>
    <Lista_de_Tarefas :tarefas="get_tarefas_filtradas()"></Lista_de_Tarefas>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
