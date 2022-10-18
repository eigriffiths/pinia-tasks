<template>
  <main>
    <!-- header -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Favs tasks</button>
    </nav>

    <!-- Task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{taskStore.totalCount}} left to do</p>
      <div v-for="task in taskStore.tasks" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{taskStore.favCount}} left to do</p>
      <div v-for="task in taskStore.favs" :key="task">
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from '@vue/reactivity'
import TaskDetails from './components/TaskDetails.vue'
import { useTaskStore } from './stores/TaskStore'

export default {
  components: {TaskDetails},
  setup(){
    const taskStore = useTaskStore()

    const filter = ref('all')

    return { taskStore, filter }
  }
}
</script>