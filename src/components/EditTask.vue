<template>
    <form class="w-96 p-8 rounded-2xl shadow-input shadow-success bg-neutral" method="dialog">
        <h1>Edit</h1>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-name">Task Name</label>
            <input type="text" class="input input-bordered w-full max-w-xs"
                v-model.trim="selectedTask.taskName_input" :placeholder="selectedTask.taskName_input == '' ? 'Please input Task Name' : ''">
        </div>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-details">Task Details</label>
            <textarea name="task-details" class="textarea textarea-bordered" v-model.trim="selectedTask.taskDetails_input" rows="4" cols="50"
                :placeholder="selectedTask.taskDetails_input == '' ? 'Please input Detials' : ''"></textarea>
        </div>
        <div class="flex justify-between">
            <button class="btn btn-error btn-outline btn-sm"
                :class="selectedTask.taskName_input === '' || selectedTask.taskDetails_input === '' ? 'btn-disabled' : ''">close</button>
            <button type="submit" class="btn btn-success btn-outline btn-sm"
                :class="selectedTask.taskName_input === '' || selectedTask.taskDetails_input === '' ? 'btn-disabled' : ''"
                @click="editTask">Edit</button>
        </div>
    </form>
</template>
<script>

export default {
    props: [
        'selectedTask'
    ],
    data() {
        return {
            editedTask: {},
        }
    },
    methods: {
        editTask() {
            this.editedTask = {
                id: this.selectedTask.id,
                taskName: this.selectedTask.taskName_input,
                taskDetails: this.selectedTask.taskDetails_input
            }
            // Emit an event with the edited task
            this.$emit('editTask', this.editedTask);
        }
    }
}
</script>
