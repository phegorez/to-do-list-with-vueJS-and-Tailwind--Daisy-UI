<template>
  <main class="flex flex-col m-10 gap-12">
    <Header @deliverInput="getHandleInput" />
    <TaskList @deleteTask="responDelete" :responTask = 'tasks' />
  </main>
</template>
<script>
import Header from './components/Header.vue'
import TaskList from './components/TaskList.vue'

export default {
  components : {
    Header, TaskList
  },
  
  data() {
    return {
      tasks : [],
    }
  },
  methods : {
    getHandleInput(deliveredInputTask) {
      this.tasks = deliveredInputTask
    },
    responDelete(taskId) {
      const findId = this.tasks.map((task) => {
        return task.id
      })
      .indexOf(taskId)

      this.tasks.splice(findId, 1)
    }
  },
  
}
</script>
