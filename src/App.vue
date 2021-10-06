<template>
  <div class="flex items-center justify-center">
    <div>
      <h1>Your tasks</h1>
      <div class="bg-white shadow-xl rounded-lg p-2 mb-8 text-lg">
        <ul :class="{ 'p-2': pendingTasks.length }">
          <li
            v-for="task in pendingTasks"
            :key="task.title"
            class="my-1 flex items-center"
          >
            <Checkbox
              v-model="task.isDone"
              type="checkbox"
              class="mr-3"
            />
            <span>{{ task.title }}</span>
          </li>
        </ul>

        <hr
          v-if="pendingTasks.length && completedTasks.length"
          class="my-1"
        >

        <ul :class="{ 'p-2': completedTasks.length }">
          <li
            v-for="task in completedTasks"
            :key="task.title"
            class="my-1 flex items-center opacity-50 line-through"
          >
            <Checkbox
              v-model="task.isDone"
              class="mr-3"
            />
            <span>{{ task.title }}</span>
          </li>
        </ul>
      </div>

      <input
        v-model="taskInput"
        type="text"
        class="bg-white mb-4"
        placeholder="Create new task..."
        @keypress.enter="createNewTask"
      >
      <button>Create Tasks</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import Checkbox from './components/Checkbox.vue'

const tasks = ref([
  { title: 'Buy Shampoo', desc: 'Buy it from DMart', isDone: false },
  { title: 'Buy Smartwatch', desc: 'Under 3000', isDone: true },
])

const pendingTasks = computed(() => tasks.value.filter(task => !task.isDone))
const completedTasks = computed(() => tasks.value.filter(task => task.isDone))

const taskInput = ref('')
const createNewTask = (e: Event) => {
  const taskTitle = (e.target as HTMLInputElement).value

  tasks.value.push({ title: taskTitle, desc: '', isDone: false })
  taskInput.value = ''
}
</script>
