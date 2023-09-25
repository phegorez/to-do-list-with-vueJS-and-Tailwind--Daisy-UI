<template>
    <form class="w-96 p-8 rounded-2xl shadow-input shadow-success bg-neutral" method="dialog">
        <h1>Edit</h1>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-name">Task Name</label>
            <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs"
                v-model="selectedTask.taskName_input" id="EditName">
        </div>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-details">Task Details</label>
            <textarea name="task-details" class="textarea textarea-bordered" v-model="selectedTask.taskDetails_input"
                id="EditDetails"></textarea>
        </div>
        <div class="flex justify-between">
            <button class="btn btn-error btn-outline btn-sm">close</button>
            <button type="submit" class="btn btn-success btn-outline btn-sm" @click="editTask">Edit</button>
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
            EditedTaskName: '',
            EditedTaskDetails: '',
        }
    },
    methods: {
        editTask() {
            // Create an object with the edited task details
            const editedTask = {
                id: this.selectedTask.id,
                taskName: this.selectedTask.taskName_input,
                taskDetails: this.selectedTask.taskDetails_input
            };

            // Emit an event with the edited task
            this.$emit('editTask', editedTask);
        }
    }
}
</script>
