<script setup>
    const props = defineProps(['tarefaTemp', 'cadastraTarefa','trocarFiltro','editaTarefaTemp']);
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
        <div class="col">
            <input
            @change="props.editaTarefaTemp"
            type="text"
            placeholder="Digite aqui a descrição da tarefa"
            class="form-control "
            >
        </div>
        <div class="col-md-1">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
                <option value="Todas">Todas</option>
                <option value="Finalizadas">Finalizadas</option>
                <option value="Pendentes">Pendentes</option>
            </select>
        </div>
        </div>
</form>
</template>    