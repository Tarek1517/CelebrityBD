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
    @click="emit('modal-close')"
  >
    <div
      class="w-full max-w-7xl bg-transparent p-8 rounded-2xl overflow-auto"
      style="max-height: 95vh"
      @click.stop
    >
      <div class="flex items-center justify-between mb-6">
        <h3 class="font-bold text-2xl text-gray-900">{{ title }}</h3>
        <button
          @click.stop="emit('modal-close')"
          aria-label="Close modal"
          class="p-2 rounded-full transition-colors"
        >
          <Icon
            name="material-symbols:close"
            class="text-rose-600 text-2xl cursor-pointer hover:text-rose-900"
          />
        </button>
      </div>
      <div>
        <slot />
      </div>
    </div>
  </div>
</template>
