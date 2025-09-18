<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro : 'Todas',
  tarefaTemp: '',
  tarefas: [
    {titulo: 'Estudar Vue.js', 
    concluida: false,
  },
    {titulo: 'Fazer compras', 
    concluida: false, 
  },
    {titulo: 'Ler um livro',
    concluida: true, 
  },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.concluida)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluida)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'Pendentes':
      return getTarefasPendentes();
    case 'Finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = (evento) => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    concluida: false,
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possue {{ getTarefasPendentes().length }} tarefas pendentes</p>

    </header>
  </div>
  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          @change="evento => estado.tarefaTemp = evento.target.value"
          :value="estado.tarefaTemp"
          type="text"
          placeholder="Digite aqui a descrição da tarefa"
          class="form-control "
        >
      </div>
      <div class="col-md-1">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control">
          <option value="Todas">Todas</option>
          <option value="Finalizadas">Finalizadas</option>
          <option value="Pendentes">Pendentes</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento => tarefa.concluida = evento.target.checked" type="checkbox" :id="tarefa.titulo" :checked="tarefa.concluida">
      <label :class="{'done': tarefa.concluida === true}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

</style>
