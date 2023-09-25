<template>
  <main class="flex flex-col m-10 gap-12">
    <Header @deliverInput="getHandleInput" />
    <TaskList @deleteTask="responDelete" @editTask="handleEditTask" :responTask = 'tasks' />
  </main>
</template>
<script>
import Header from './components/Header.vue'
import TaskList from './components/TaskList.vue'

const LocalKey = 'taskStorage'

export default {
  components : {
    Header, TaskList
  },
  
  data() {
    return {
      tasks : [],
    }
  },
  created() {
    // Load tasks from localStorage on component creation
    const savedTasks = localStorage.getItem(LocalKey);
    if (savedTasks) {
      this.tasks = JSON.parse(savedTasks);
    }
  },
  methods : {
    getHandleInput(deliveredInputTask) {
      this.tasks = deliveredInputTask
      this.saveTasksToLocalStorage()
    },
    responDelete(taskId) {
      const findId = this.tasks.map((task) => {
        return task.id
      })
      .indexOf(taskId)

      this.tasks.splice(findId, 1)
      this.saveTasksToLocalStorage()
    },
    handleEditTask(editedTask) {
      const taskIndex = this.tasks.findIndex(task => task.id === editedTask.id);

      if (taskIndex !== -1) {
        this.tasks[taskIndex].taskName_input = editedTask.taskName;
        this.tasks[taskIndex].taskDetails_input = editedTask.taskDetails;

        // Save updated tasks to local storage
        this.saveTasksToLocalStorage();
      }
    },
    saveTasksToLocalStorage() {
      localStorage.setItem(LocalKey, JSON.stringify(this.tasks));
    },
  },
  
}
</script>
