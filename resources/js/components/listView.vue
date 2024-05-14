<template>
    <div class="mt-4">
         <h4>Lista de Tarefas</h4>
        <hr class="w-50 m-auto mb-3" />
        <table class="table">
            <thead class="thead-light">
                <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Nome</th>
                    <th scope="col">Descrição</th>
                    <th scope="col">Status</th>
                    <th scope="col">Ações</th>
                </tr>
            </thead>
            <list-item
                :task="taks"
                v-on:itemchanged="$emit('reloadlist')"
                v-for="taks in tasks_itm"
                :key="taks.id"
                class="m-auto my-1 text-justify text-wrap"
            />
        </table>
    </div>

</template>

<script>
import listItem from "./listItem";

export default {
    components: {
        listItem,
    },
    data: function() {
        return {
            tasks: []
        };
    },
        props: ["tasks_itm"]
        
};
</script>

<style scoped></style>
