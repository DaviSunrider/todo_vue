<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import ListaTarefas from "./components/ListaTarefas.vue";

const estado = reactive({
  filtro: "todas",
  tarefaTemp: "",
  tarefa: [
    { titulo: "Estudar Vue", finalizada: false },
    { titulo: "Estudar JavaScript", finalizada: false },
    { titulo: "Estudar CSS", finalizada: false },
    { titulo: "Estudar HTML", finalizada: false },
    { titulo: "Estudar Node", finalizada: false },
    { titulo: "Estudar MongoDB", finalizada: false },
    { titulo: "Estudar Express", finalizada: false },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefa.filter((tarefa) => !tarefa.finalizada);
};

const getTarefasFinalizadas = () => {
  return estado.tarefa.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefa;
  }
};

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefa.push(tarefaNova);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario
      :trocar-filtro="(evento) => (estado.filtro = evento.target.value)"
      :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="(evento) => (estado.tarefaTemp = evento.target.value)"
      :cadastra-tarefas="cadastraTarefa"
    />
    <ListaTarefas :tarefa="getTarefasFiltradas" />
  </div>
</template>
