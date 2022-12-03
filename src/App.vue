<script>
import TaskTracker from './components/TaskTracker.vue';
export default {
  name: 'App',
  components: {
    TaskTracker,
  }
}
</script>

<template>
  <div class="bg-neutral-100 min-h-screen flex flex-col items-center">
    <main class="max-w-2xl w-full p-3">
      <TaskTracker />
    </main>
  </div>
</template>
