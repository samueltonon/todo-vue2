<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',

    tarefaTemporaria: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Andar de skate',
        finalizada: true,
      }
    ]
  });

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  };

  const getTarefasConcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  };

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch ( filtro ){
      case 'pendentes':
        return getTarefasPendentes();
      case 'concluidas':
        return getTarefasConcluidas();
        default:
          return estado.tarefas;
    }
  };

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemporaria,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemporaria = '';
  };
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


