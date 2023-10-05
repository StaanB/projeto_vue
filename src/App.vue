<script setup>
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Form.vue";
import ListaDeTarefas from "./components/ListaDeTarefas.vue";


import { reactive } from 'vue';

const estado = reactive({
  filtro: "todas",
  tarefaTemporaria: "",
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: "Estudar SASS",
      finalizada: false
    },
    {
      titulo: "Go to gym",
      finalizada: true
    }
  ]
})

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemporaria = ''
}

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes()
    case 'finalizadas':
      return getTarefasFinalizadas()
    default:
      return estado.tarefas
  }
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />

    <Formulario :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"/>

    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>


  </div>
</template>