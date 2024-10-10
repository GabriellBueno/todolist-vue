<script setup>
const props = defineProps(['cadastra_Tarefa', 'tarefa_Temp', 'trocar_filtro', 'edita_Tarefa_Temp']) 

</script>
]


<template>
    <form @submit.prevent="props.cadastra_Tarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefa_temp" @change="props.edita_Tarefa_Temp" required
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocar_filtro" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>