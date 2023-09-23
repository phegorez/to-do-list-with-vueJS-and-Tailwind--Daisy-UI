<template>
    <section class="flex flex-wrap gap-8 justify-center py-4 shadow-input shadow-success rounded-md"
        v-if="responTask.length > 0">
        <div class="card w-96 bg-neutral text-neutral-content" v-for="(task, id) in responTask" :key="task.id">
            <div class="card-body items-center text-center">
                <h2 class="card-title">{{ task.taskName_input }}</h2>
                <p>{{ task.taskDetails_input }}</p>
                <div class="card-actions justify-end flex items-center gap-2">
                    <button class="btn btn-primary" @click="openEditModal(task.id)">Edit</button>
                    <dialog :id="'editModal-' + task.id" class="modal">
                        <EditTask :selectedTask = 'task' />
                    </dialog>
                    <button class="btn btn-ghost" @click="deleteTask(task.id)">Delete</button>
                    <div class="flex flex-col">
                        <label for="checkStatus">Success</label>
                        <input type="checkbox" class="checkbox" v-model="task.status">
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import EditTask from './EditTask.vue'
export default {
    components : {
        EditTask
    },
    props: [
        'responTask'
    ],
    methods: {
        deleteTask(taskId) {
            this.$emit('deleteTask', taskId)
        },
        openEditModal(taslId) {
            const modalId = 'editModal-' + taslId
            const modal = document.getElementById(modalId)
            modal.showModal()
        }
    }
}
</script>