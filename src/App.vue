<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Voce possui {{ get_tarefas_pendentes().length }} Tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastra_tarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefa_temp" @change="evento => estado.tarefa_temp = evento.target.value" required
            type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in get_tarefas_filtradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
          :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
