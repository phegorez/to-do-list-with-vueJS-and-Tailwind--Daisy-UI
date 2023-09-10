<template>
  <section class="container flex-col justify-center items-center h-screen m-auto">
    <h1 class="font-Kanit font-bold text-3xl mt-3">To-Do List 📑</h1>
    <!-- Add new task form -->
    <div class="flex flex-row items-center justify-center gap-10 mt-3">
      <input type="text" class="input input-bordered w-full max-w-xs" placeholder="Please write your task"
        v-model="inputTask">
      <button type="button" class="btn btn-primary" @click="addNewTask">Add new task</button>
    </div>


    <!-- Task List -->
    <table class="table">

      <thead>
        <tr>
          <th>Task Name</th>
          <th>Status</th>
          <th>Delete</th>
          <th>Edit</th>
        </tr>
      </thead>

      <tbody>
        <tr :class="task.Status ? 'bg-[#0E402D]' : 'bg-base-200'" class="" v-for="(task, id) in tasks" :key="id">
          <td>
            <p :style="task.Status ? { textDecoration: 'line-through' } : ''" :class="task.Status ? 'italic' : ''" class="text-xl capitalize">{{ task.Task_Name }}</p>
          </td>
          <td>
            <input type="checkbox" name="checkbox" v-model="task.Status" class="checkbox">
          </td>
          <td>
            <button type="button" class="btn btn-outline btn-error" @click="delTask(task.id)">Delete Task</button>
          </td>
          <td>
            <button class="btn btn-outline btn-info" onclick="my_modal_1.showModal()">Edit</button>

            <dialog id="my_modal_1" class="modal">
              <div class="modal-box">
                <h3 class="font-bold text-lg">Edit your task</h3>
                <input type="text" class="input input-bordered w-full max-w-xs" v-model="task.Task_Name" placeholder="Edit">
                <div class="modal-action">
                  <form method="dialog">
                    <!-- if there is a button in form, it will close the modal -->
                    <button class="btn btn-primary">Save</button>
                  </form>
                </div>
              </div>
            </dialog>

          </td>
        </tr>
      </tbody>

    </table>
  </section>
</template>
<script>
export default {
  data() {
    return {
      inputTask: '',
      tasks: [],
    }
  },
  methods: {
    addNewTask() {
      if (this.inputTask == '') {
        alert('Please add your task')
      } else {
        this.tasks = [
          {
            id: new Date().getTime(),
            Task_Name: this.inputTask,
            Status: false
          },
          ...this.tasks
        ]
        this.inputTask = ''
      }
    },
    delTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
  },
}
</script>
<style scoped="">
.task-form {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}
</style>