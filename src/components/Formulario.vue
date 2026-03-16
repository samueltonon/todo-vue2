<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemp']);
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria"
                    @change="props.editaTarefaTemp" required type="text"
                    placeholder="Digite a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="concluidas">Concluídas</option>
                </select>
            </div>
        </div>
    </form>
</template>