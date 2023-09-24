<template>
    <header class="flex justify-between items-center">
        <h1 class="text-2xl font-bold">To-Do List</h1>
        <button class="btn btn-success btn-outline" @click="openInputModal">Add Task</button>
        <dialog id="inputModal" class="modal">
            <InputTask @inputTask="getInputTask" :backToInput="openInputModal"/>
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
        },
        openInputModal() {
            const inputmodal = document.getElementById('inputModal')
            inputmodal.showModal()
        }
    }
    
}
</script>
