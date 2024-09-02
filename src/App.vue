<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
    {
        titulo: 'MOLDE DE TAREFAS - DELETE ALL IN THIS ICON -------------------------------------->',
        finalizada: false,
      },
      {
        titulo: 'Estudar Python | Udemy',
        finalizada: false,
      },
      {
        titulo: 'Estudar Js Practicals | Udemy',
        finalizada: false,
      },
      {
        titulo: 'Estudar Desenvolvimento Fullstack | EBAC',
        finalizada: false,
      },
      {
        titulo: 'Estudar Ingles | WiseUp',
        finalizada: false,
      },
      {
        titulo: 'Ir para academia',
        finalizada: false,
      }
    ]
  }) 

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }

  const removeTarefa = (index) => {
    estado.tarefas.splice (index, 1);
  };
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" :removeTarefa="removeTarefa" />
  </div>
</template>

