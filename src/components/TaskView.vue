<script>
  import TaskCard from './TaskCard.vue';
  import TaskEmpty from './TaskEmpty.vue';
  export default {
    name: 'TaskView',
    props: {
      tasks: Array,
    },
    components: {
      TaskCard,
      TaskEmpty,
    },
    methods: {
      onDeleteClick(id) {
        this.$emit('onDelete', id);
      },
      onDoneClick(id) {
        this.$emit('onDone', id);
      },
    },
    emits: ['onDelete', 'onDone'],
  }
</script>

<template>
  <div v-if="(tasks.length >= 1)" class="md:grid md:grid-cols-2 md:gap-x-4">
    <template v-for="task in tasks">
      <TaskCard 
        :id="task.id" 
        :name="task.name" 
        :priority="task.priority" 
        :description="task.description"
        :doneAt="task.doneAt"
        @on-delete-click="onDeleteClick"
        @on-done-click="onDoneClick"
      />
    </template>
  </div>
  <TaskEmpty v-if="(tasks.length === 0)" />
</template>