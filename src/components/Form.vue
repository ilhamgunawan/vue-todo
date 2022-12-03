<script>
  export default {
    name: 'Form',
    methods: {
      onSubmit(event) {
        event.preventDefault();
        this.$emit('onSubmit', event);
      }
    },
    emits: ['onSubmit']
  }
</script>

<template>
  <form class="" :onSubmit="onSubmit">
    <div class="flex flex-col mb-4">
      <h2 class="text-center text-lg font-bold">Create new task</h2>
    </div>
    <div class="flex flex-col mb-4">
      <label for="taskName">Task name</label>
      <input
        class="border border-gray-200 rounded-md p-2 mt-2"
        id="taskName"
        name="taskName" 
        type="text" 
        placeholder="Input task name"
        required
      />
    </div>
    <div class="flex flex-col mb-4">
      <label for="taskPriority">Priority</label>
      <select
        class="border border-gray-200 rounded-md p-2 mt-2"
        id="taskPriority"
        name="taskPriority"
        defaultValue="P0"
        required
      >
        <option value="P0">P0</option>
        <option value="P1">P1</option>
        <option value="P2">P2</option>
      </select>
    </div>
    <div class="flex flex-col mb-8">
      <label for="taskDescription">Description (optional)</label>
      <textarea 
        class="border border-gray-200 rounded-md p-2 mt-2"
        id="taskDescription"
        name="taskDescription"
      />
    </div>
    <div class="flex flex-col">
      <button class="w-fit self-end bg-sky-600 text-white py-2 px-4 rounded-md shadow" type="submit">Create</button>
    </div>
  </form>
</template>
