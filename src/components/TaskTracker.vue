<script>
  import { v4 as uuidv4 } from 'uuid';
  import Form from './Form.vue';
  import TaskView from './TaskView.vue';
  import Modal from './Modal.vue';
  export default {
    name: 'TaskTracker',
    components: {
      Form,
      TaskView,
      Modal,
    },
    data() {
      const tasksJson = localStorage.getItem('tasks');
      const initialData = tasksJson ? JSON.parse(tasksJson) : [];
      return {
        tasks: initialData,
        isShowModalForm: false,
      }
    },
    methods: {
      toggleModalForm() {
        this.isShowModalForm = !this.isShowModalForm;
      },
      addTask(task) {
        this.tasks = [task, ...this.tasks];
      },
      handleSubmit(event) {
        const formData = new FormData(event.target);
        const name = formData.get('taskName');
        const priority = formData.get('taskPriority');
        const description = formData.get('taskDescription');
        this.addTask({
          id: uuidv4(),
          name,
          priority,
          description,
          createdAt: new Date().toISOString(),
          doneAt: null,
        });
        this.toggleModalForm();
      },
      handleDelete(id) {
        const newTasks = this.tasks.filter(task => task.id !== id);
        this.tasks = newTasks;
      },
      handleDone(id) {
        this.tasks = this.tasks.map(task => {
          if (task.id === id) {
            return {
              ...task,
              doneAt: new Date().toISOString(),
            };
          } else {
            return task;
          }
        });
      },
      saveToStorage(tasks) {
        const serializedTasks = JSON.stringify(tasks);
        localStorage.setItem('tasks', serializedTasks);
      },
    },
    watch: {
      tasks(newTasks, oldTasks) {
        this.saveToStorage(newTasks);
      }
    }
  }
</script>

<template>
  <button 
    @click="toggleModalForm"
    class="w-fit self-end bg-sky-600 text-white py-2 px-4 mb-5 rounded-md shadow"
  >
    Create Task
  </button>
  <TaskView 
    :tasks="tasks" 
    @on-delete="handleDelete"
    @on-done="handleDone"
  />
  <Modal :isShowModal="isShowModalForm" @on-overlay-click="toggleModalForm">
    <Form @on-submit="handleSubmit" />
  </Modal>
</template>