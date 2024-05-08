<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import List from "./components/List.vue";

const estado = reactive({
  filtro: "todas",
  tarefaTemp: "",
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar Sass",
      finalizada: false,
    },
    {
      titulo: "Ir na academia",
      finalizada: true,
    },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada === false);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <Header :tarefas-pendentes="getTarefasPendentes().length" />
    <Form
      :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="(evento) => (estado.tarefaTemp = evento.target.value)"
      :cadastra-tarefa="cadastraTarefa"
      :trocar-filtro="(evento) => (estado.filtro = evento.target.value)"
    />
    <List :tarefas="getTarefasFiltradas()" />
  </div>
</template>
