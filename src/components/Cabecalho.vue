<script setup>
    const props = defineProps(['tarefas_Pendentes'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <p>
            Voce possui {{ props.tarefas_Pendentes }} Tarefas pendentes
        </p>
    </header>
</template>