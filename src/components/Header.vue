<template>
    <header class="flex justify-between items-center">
        <h1>To-Do List</h1>
        <button class="btn btn-success btn-outline" onclick="inputModal.showModal()">Add Task</button>

        <dialog id="inputModal" class="modal">
            <InputTask @inputTask="getInputTask"/>
        </dialog>
    </header>
</template>

<script>
    import InputTask from './InputTask.vue';
export default {
    
    components: {
        InputTask
    },
    data() {
        return {
            handleInputTask : [],
        }
    },
    methods : {
        getInputTask(inputTask) {
            this.handleInputTask = inputTask
            this.$emit('deliverInput', this.handleInputTask)
        }
    }
    
}
</script>
