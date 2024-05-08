<script setup>
const props = defineProps(["tarefas"]);
</script>

<template>
  <ul class="list-group mt-4" v-if="tarefas.length > 0">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        @change="(evento) => (tarefa.finalizada = evento.target.checked)"
        :checked="tarefa.finalizada"
        :id="tarefa.titulo"
        type="checkbox"
      />
      <label
        :class="{ done: tarefa.finalizada }"
        class="ms-2"
        :for="tarefa.titulo"
      >
        {{ tarefa.titulo }}</label
      >
    </li>
  </ul>

  <p class="mt-4" v-else>Não existem tarefas Pendentes</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
