<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.getTarefasFiltradas()" :key="tarefa.titulo">
            <input @change="event => tarefa.concluida = event.target.checked" type="checkbox" :id="tarefa.titulo" :checked="tarefa.concluida">
            <label :class="{'done': tarefa.concluida === true}" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<script setup>
const props = defineProps({
    getTarefasFiltradas: {
        type: Function,
        required: true
    }
});
</script>