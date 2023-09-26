<template>
  <main class="flex flex-col m-10 gap-12">
    <Header @deliverInput="getHandleInput" />
    <TaskList @deleteTask="responDelete" @editTask="handleEditTask" :responTask='tasks' />
  </main>
</template>
<script>
import Header from './components/Header.vue'
import TaskList from './components/TaskList.vue'

const LocalKey = 'taskStorage'

export default {
  components: {
    Header, TaskList
  },

  data() {
    return {
      tasks: [],
    }
  },
  created() {
    // Load tasks from localStorage on component creation
    const savedTasks = localStorage.getItem(LocalKey);
    if (savedTasks) {
      this.tasks = JSON.parse(savedTasks);
    }
  },
  methods: {
    getHandleInput(deliveredInputTask) {
      
      // Ensure this.tasks is an array
      if (!Array.isArray(this.tasks)) {
        this.tasks = [];
      }

      if (Array.isArray(deliveredInputTask)) {
        // If deliveredInputTask is an array
        for (const task of deliveredInputTask) {
          // Check if task already exists in this.tasks by comparing IDs
          const existingTask = this.tasks.find(existing => existing.id === task.id);

          if (!existingTask) {
            // If the task doesn't exist, add it to the tasks array
            this.tasks.push(task);
          }
        }
      } else {
        // If deliveredInputTask is a single object
        const existingTask = this.tasks.find(existing => existing.id === deliveredInputTask.id);

        if (!existingTask) {
          // If the task doesn't exist, add it to the tasks array
          this.tasks.push(deliveredInputTask);
        }
      }

      // Save the updated tasks to local storage
      this.saveTasksToLocalStorage();
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
