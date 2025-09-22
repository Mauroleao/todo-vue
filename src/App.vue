<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  filtro: 'Todas',
  tarefaTemp: '',
  tarefas: [
    { titulo: 'Estudar Vue.js', concluida: false },
    { titulo: 'Fazer compras', concluida: false },
    { titulo: 'Ler um livro', concluida: true },
  ],
});


const getTarefasPendentes = () => estado.tarefas.filter(tarefa => !tarefa.concluida);
const getTarefasFinalizadas = () => estado.tarefas.filter(tarefa => tarefa.concluida);
const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'Pendentes':
      return getTarefasPendentes();
    case 'Finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = () => {
  if (!estado.tarefaTemp.trim()) return;
  estado.tarefas.push({ titulo: estado.tarefaTemp, concluida: false });
  estado.tarefaTemp = '';
};

const editaTarefaTemp = (evento) => {
  estado.tarefaTemp = evento.target.value;
};

const trocarFiltro = (evento) => {
  estado.filtro = evento.target.value;
};

</script>

<template>
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario
      :tarefaTemp="estado.tarefaTemp"
      :editaTarefaTemp="editaTarefaTemp"
      :cadastraTarefa="cadastraTarefa"
      :trocarFiltro="trocarFiltro"
    />
    <ListaDeTarefas :getTarefasFiltradas="getTarefasFiltradas" />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

</style>
