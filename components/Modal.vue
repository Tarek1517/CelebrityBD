<script setup>
const props = defineProps({
  isOpen: Boolean,
  title: String,
});

const emit = defineEmits(["modal-close"]);
</script>

<template>
  <div
    v-if="isOpen"
    class="fixed top-0 left-0 right-0 bottom-0 bg-black/80 w-full h-screen flex items-center justify-center z-[99999] p-4"
  >
    <div
      class="w-full max-w-5xl min-h-[10rem] bg-white p-8 shadow-lg rounded-md overflow-auto"
      style="max-height: 90vh"
    >
      <div class="flex items-center justify-between mb-4">
        <h3 class="font-medium text-lg sm:text-xl">{{ title }}</h3>
        <button @click.stop="emit('modal-close')" aria-label="Close modal">
          <Icon
            name="material-symbols:close"
            class="text-primary text-3xl sm:text-4xl cursor-pointer"
          />
        </button>
      </div>
      <div>
        <slot />
      </div>
    </div>
  </div>
</template>
