<template>
    <form class="w-96 p-8 rounded-2xl shadow-input shadow-success bg-neutral" method="dialog">
        <dialog id="alertBox" class="modal">
            <form method="dialog"
                class="w-96 p-8 rounded-2xl shadow-input shadow-warning bg-neutral flex flex-col gap-8 items-center">
                <h1 class="text-2xl" v-if="!inputTask.taskName_input && !inputTask.taskDetails_input">Your Information is
                    empty</h1>
                <h1 class="text-2xl" v-else-if="!inputTask.taskName_input">Your Task Name is empty</h1>
                <h1 class="text-2xl" v-else-if="!inputTask.taskDetails_input">Your Task Details is empty</h1>
                <div class="flex gap-5">
                    <button class="btn btn-info btn-outline btn-sm" @click="backToInput">back</button>
                    <button class="btn btn-error btn-outline btn-sm">close</button>
                </div>
            </form>
        </dialog>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-name">Task Name</label>
            <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs"
                v-model="inputTask.taskName_input">
        </div>
        <div class="flex flex-col gap-4 mb-4">
            <label for="task-details">Task Details</label>
            <textarea name="task-details" class="textarea textarea-bordered"
                v-model="inputTask.taskDetails_input"></textarea>
        </div>
        <div class="flex justify-between">
            <button class="btn btn-error btn-outline btn-sm">close</button>
            <button type="submit" class="btn btn-success btn-outline btn-sm" @click="addTask">add</button>
        </div>
    </form>
</template>
<script>
export default {
    props : {
        backToInput : {
            type : Function
        }
    },
    data() {
        return {
            Tasks: [],
            inputTask: {
                taskName_input: '',
                taskDetails_input: '',
                status: false
            },
        }
    },
    methods: {
        addTask() {
            if (!this.inputTask.taskName_input || !this.inputTask.taskDetails_input) {
                const alertBox = document.getElementById('alertBox');
                alertBox.showModal();
            }
            else {
                //Add id prop to inputTask
                this.inputTask.id = new Date().getTime()
                //Push inputTask to Tasks Array
                this.Tasks.push({ ...this.inputTask })
                //Reset input task name after submit
                this.inputTask.taskName_input = ''
                //Reset input task details after submit
                this.inputTask.taskDetails_input = ''
                //Passing Task data by event inputTask to Header Component
                this.$emit('inputTask', this.Tasks)
            }
        },
    }
}
</script>
