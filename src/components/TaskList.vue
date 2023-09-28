<template>
    <section v-if="responTask.length === 0">
        Not have any Task
    </section>
    <section class="flex flex-wrap gap-8 justify-center py-4 shadow-input shadow-primary rounded-md"
        v-else-if="responTask.length > 0">
        <div class="cursor-pointer card w-96 bg-neutral text-neutral-content hover:shadow-input"
            :class="task.status ? 'hover:shadow-success' : 'hover:shadow-error'" v-for="(task, id) in responTask"
            :key="task.id">
            <div class="card-body items-start text-start relative">
                <div class="flex flex-col absolute top-4 right-4">
                    <input type="checkbox" :class="task.status ? 'checkbox  checkbox-success' : 'checkbox'"
                        v-model="task.status" @change="handleStatusChange(task)">
                </div>
                <h2 class="card-title" :class="task.status ? 'italic line-through' : ''">{{ task.taskName_input }}</h2>
                <p :class="task.status ? 'italic line-through' : ''">{{ task.taskDetails_input }}</p>
                <div class="card-actions flex items-center gap-2">
                    <button class="btn btn-primary btn-sm" @click="openEditModal(task.id)"
                        :class="task.status ? 'btn-disabled' : ''">Edit</button>

                    <!-- Open it if user not input any input from EditTask component -->
                    <dialog :id="'editModal-' + task.id" class="modal">
                        <EditTask :selectedTask='task' @editTask="handleEditTask" />
                    </dialog>
                    <button class="btn btn-error btn-outline btn-sm" @click="deleteTask(task.id)"
                        :class="task.status ? 'btn-disabled' : ''">Delete</button>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import EditTask from './EditTask.vue'
export default {
    components: {
        EditTask
    },
    props: [
        'responTask'
    ],
    methods: {
        deleteTask(taskId) {
            this.$emit('deleteTask', taskId)
        },
        openEditModal(taskId) {
            const modalId = 'editModal-' + taskId
            const modal = document.getElementById(modalId)
            modal.showModal()
        },
        handleEditTask(editedTask) {
            this.$emit('editTask', editedTask)
        },
        handleStatusChange(task) {
            // Update the task status in local storage
            const savedTasks = JSON.parse(localStorage.getItem('taskStorage')) || [];
            const updatedTasks = savedTasks.map((savedTask) =>
                savedTask.id === task.id ? { ...savedTask, status: task.status } : savedTask
            );
            localStorage.setItem('taskStorage', JSON.stringify(updatedTasks));
        },
    }
}
</script>