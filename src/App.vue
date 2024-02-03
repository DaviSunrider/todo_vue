<script setup>
import { reactive } from "vue";

const estado = reactive({
  tarefa: [
    { titulo: "Estudar Vue", finalizada: false },
    { titulo: "Estudar JavaScript", finalizada: false },
    { titulo: "Estudar CSS", finalizada: true },
    { titulo: "Estudar HTML", finalizada: false },
    { titulo: "Estudar Node", finalizada: true },
    { titulo: "Estudar MongoDB", finalizada: false },
    { titulo: "Estudar Express", finalizada: true },
  ],
});
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui 7 tarefas pendentes</p>
    </header>
    <form>
      <div class="row">
        <div class="col">
          <input
            type="text"
            placeholder="Digite aqui a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in estado.tarefa">
        <input
          :checked="tarefa.finalizada"
          :id="tarefa.titulo"
          type="checkbox"
        />
        <label
          :class="{ done: tarefa.finalizada }"
          class="ms-3"
          :for="tarefa.titulo"
        >
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
