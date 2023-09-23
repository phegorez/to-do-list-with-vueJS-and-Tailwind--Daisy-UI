<template>
    <form class="w-96 p-8 rounded-2xl shadow-input shadow-success bg-neutral" method="dialog" @submit="addTask">
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-name">Task Name</label>
            <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs"
                v-model="inputTask.taskName_input">
        </div>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-details">Task Details</label>
            <textarea name="task-details" class="textarea textarea-bordered" v-model="inputTask.taskDetails_input"></textarea>
        </div>
        <div class="flex justify-between">
            <button class="btn btn-error btn-outline btn-sm">close</button>
            <button type="submit" class="btn btn-success btn-outline btn-sm">add</button>
        </div>
    </form>
</template>
<script>
export default {
    data() {
        return {
            Tasks: [],
            inputTask: {
                taskName_input: '',
                taskDetails_input: '',
                status : false
            },
        }
    },
    methods: {
        addTask() {
            //Add id prop to inputTask
            this.inputTask.id = new Date().getTime()
            //Push inputTask to Tasks Array
            this.Tasks.push({...this.inputTask})
            //Reset input task name after submit
            this.inputTask.taskName_input = ''
            //Reset input task details after submit
            this.inputTask.taskDetails_input = ''
            //Passing Task data by event inputTask to Header Component
            this.$emit('inputTask', this.Tasks)
        }
    }
}
</script>
