<script>
import { X } from 'lucide-vue-next';
  export default {
    props: {
      isShowModal: {
        type: Boolean,
        default: false,
      },
    },
    components: { X },
    methods: {
      onOverlayClick() {
        this.$emit('onOverlayClick');
      }
    }
  }
</script>

<template>
  <div v-if="isShowModal" class="backdrop fixed inset-0 flex flex-col items-center justify-center">
    <div class="bg-white p-3 w-11/12 sm:w-96 relative shadow-md rounded-md z-10">
      <button @click="onOverlayClick" class="absolute top-3 right-3">
        <X :size="18" />
      </button>
      <slot />
    </div>
    <div @click="onOverlayClick" class="absolute inset-0" />
  </div>
</template>

<style scoped>
.backdrop {
  background-color: rgba(0,0,0,.3);
  -webkit-backdrop-filter: blur(3px);
  backdrop-filter: blur(3px);
}
</style>