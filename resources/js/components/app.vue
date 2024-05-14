<template>
    <div class="container w-100 m-auto text-center mt-3">
        <transition name="modal">
				<div class="modal-mask" v-if="showModal">
					<modal @close="closeModal"/>
				</div>
			</transition>
        <h1 class="text-danger">Todo List</h1>
        <list-view
            :tasks_itm="tasks"
            v-on:reloadlist="getItems()"
            class="text-center"
        />
    </div>
    
</template>

<script>

import listView from "./listView";
import modal from "./modal.vue";

const showModal = false;

export default {
    components: {
        listView,
        modal
    },

    data: function() {
        return {
            tasks: []
        };
    },
    mounted() {
      this.getItems();
    },
    methods: {
        closeModal(){
			showModal = false;
		},
        getItems() {
            axios
                .get("api/tasks")
                .then(res => {
                    this.tasks = res.data;
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    created() {
        this.getItems();
    }
};
</script>

<style scoped></style>
