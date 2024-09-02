<script setup>
    const trashIcon = new URL('../assets/trash-2.svg', import.meta.url).href;
    const props = defineProps(['tarefas', 'removeTarefa'])
</script>

<template>
    <ul class="list-group mt-4">
        <li 
        class="list-group-item custom-list-item-2 d-flex justify-content-between align-items-center" 
        v-for="(tarefa, index) in props.tarefas" 
        :key="index">
        <div class="d-flex align-items-center">
            <input @change="evento => tarefa.finalizada = evento.target.checked"
            :checked="tarefa.finalizada"
            :id="`tarefa-${index}`"
            type="checkbox"/>
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="`tarefa-${index}`">
            {{ tarefa.titulo }}
        </label>
        </div>
        <button @click="props.removeTarefa(index)" class="btn btn-sm custom-btn">
        <img :src="trashIcon" alt="Remover tarefa" class="trash-icon"/>
        </button>
    </li>
    <li class="list-group-item custom-list-item" v-if="props.tarefas.filter(tarefa => !tarefa.finalizada).length === 0">
        Não existem tarefas pendentes
    </li>
    </ul>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }

    .trash-icon {
    width: 16px;
    height: 16px;
    }

    .custom-list-item {
        background-color: #CCD0CF;
        border: 1px solid #ced4da;
        padding: 6px;
        margin-top: 25px;
        border-radius: 4px;
        color: #06141B;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1rem;
        font-weight: 400;
        line-height: 1.5;
        transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    }
</style>