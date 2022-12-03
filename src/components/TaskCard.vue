<script>
  import { Trash2, CheckCircle } from 'lucide-vue-next';
  export default {
    name: 'TaskCard',
    props: {
      id: String,
      name: String,
      priority: String,
      description: String,
      doneAt: String,
    },
    components: { Trash2, CheckCircle },
    methods: {
      onDeleteClick(id) {
        this.$emit('onDeleteClick', id);
      },
      onDoneClick(id) {
        if (!this.doneAt) {
          this.$emit('onDoneClick', id);
        }
      },
    },
    emits: ['onDeleteClick', 'onDoneClick'],
  }
</script>

<template>
  <div class="bg-white h-40 mb-5 overflow-hidden flex flex-col justify-between shadow-md rounded-md">
    <div class="p-3">
      <div class="flex flex-row justify-between">
        <h3 class="font-semibold truncate mr-1">{{ name }}</h3>
        <div>
          <span
            v-if="(Boolean(doneAt))"
            class="bg-green-400 text-xs text-white font-semibold p-1 rounded mr-2"
          >
            Done
          </span>
          <span 
            class="text-xs text-white font-semibold p-1 rounded"
            :class="{
              'bg-red-600': priority === 'P0',
              'bg-orange-400': priority === 'P1',
              'bg-gray-400': priority === 'P2',
            }"
          >
            {{ priority }}
          </span>
        </div>
      </div>
      <div class="mt-2">
        <p class="text-sm text-neutral-500 description">{{ description }}</p>
      </div>
    </div>
    <div class="flex justify-between items-center">
      <button
        @click="onDeleteClick(id)" 
        class="btn-delete hover:bg-neutral-50 p-3 flex-1 flex flex-row justify-center border-t border-r text-sm text-neutral-600"
      >
        <Trash2
          class="delete mr-1"
          :size="18"
        />
        <span class="delete">Delete</span>
      </button>
      <button
        @click="onDoneClick(id)"
        class="p-3 flex-1 flex flex-row justify-center border-t text-sm text-neutral-600"
        :class="{
          'cursor-not-allowed': Boolean(doneAt),
          'bg-neutral-100': Boolean(doneAt),
          'text-neutral-300': Boolean(doneAt),
          'btn-done': !doneAt,
          'hover:bg-neutral-50': !doneAt,
          'text-neutral-600': !doneAt,
        }"
      >
        <CheckCircle
          class="done mr-1"
          :size="18"
        />
        <span class="done">Done</span>
      </button>
    </div>
  </div>
</template>

<style scoped>
.description {
  word-break: break-word;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}

.btn-delete:hover .delete {
  --tw-text-opacity: 1;
  color: rgb(248 113 113 / var(--tw-text-opacity));
}

.btn-done:hover .done {
  --tw-text-opacity: 1;
  color: rgb(22 163 74 / var(--tw-text-opacity));
}
</style>