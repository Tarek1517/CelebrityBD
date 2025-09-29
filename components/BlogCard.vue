<script setup>
defineProps({
  update: {
    type: Object,
    required: true,
  },
});

// Helper functions
const formatMonth = (date) => {
  return new Date(date).toLocaleString("default", { month: "short" });
};

const formatDay = (date) => {
  return new Date(date).getDate();
};

const formatYear = (date) => {
  return new Date(date).getFullYear();
};

const formatRelativeDate = (date) => {
  const now = new Date();
  const publishDate = new Date(date);
  const diffTime = Math.abs(now - publishDate);
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

  if (diffDays === 1) return "Today";
  if (diffDays === 2) return "Yesterday";
  if (diffDays < 7) return `${diffDays - 1} days ago`;
  if (diffDays < 30) return `${Math.floor(diffDays / 7)} weeks ago`;
  return `${Math.floor(diffDays / 30)} months ago`;
};
</script>

<template>
  <div
    class="group bg-white rounded-3xl overflow-hidden flex flex-col h-full shadow-lg hover:shadow-2xl transition-all duration-500 border border-gray-200/50 hover:border-pink-200/70 hover:-translate-y-2"
  >
    <!-- Image Container -->
    <div class="relative overflow-hidden h-60">
      <img
        :src="update.image"
        :alt="update.title"
        class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
      />
      <div
        class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"
      ></div>

      <!-- Category Badge -->
      <div class="absolute top-4 left-4">
        <span
          class="inline-flex items-center px-4 py-2 bg-gradient-to-r from-pink-500 to-purple-600 text-white rounded-full text-sm font-semibold shadow-lg backdrop-blur-sm"
        >
          {{ update.category }}
        </span>
      </div>

      <!-- Publish Date -->
      <div class="absolute top-4 right-4">
        <div
          class="flex flex-col items-center justify-center bg-black/70 text-white rounded-xl py-2 px-3 backdrop-blur-sm border border-white/20"
        >
          <span class="text-xs font-semibold uppercase leading-none">{{
            formatMonth(update.publishDate)
          }}</span>
          <span class="text-lg font-bold text-pink-300">{{
            formatDay(update.publishDate)
          }}</span>
          <span class="text-xs leading-none mt-1">{{
            formatYear(update.publishDate)
          }}</span>
        </div>
      </div>

      <!-- Engagement Stats -->
      <div
        class="absolute bottom-4 left-4 flex items-center space-x-4 text-white text-sm"
      >
        <div
          class="flex items-center space-x-1 bg-black/40 backdrop-blur-sm px-3 py-1 rounded-full"
        >
          <Icon name="heroicons:eye" class="w-4 h-4" />
          <span>{{ update.views }}</span>
        </div>
        <div
          class="flex items-center space-x-1 bg-black/40 backdrop-blur-sm px-3 py-1 rounded-full"
        >
          <Icon name="heroicons:heart" class="w-4 h-4 text-red-400" />
          <span>{{ update.likes }}</span>
        </div>
      </div>
    </div>

    <!-- Content -->
    <div class="p-6 flex flex-col flex-grow">
      <!-- Title -->
      <h3
        class="text-xl font-bold text-gray-900 mb-3 line-clamp-2 group-hover:text-transparent group-hover:bg-clip-text group-hover:bg-gradient-to-r group-hover:from-pink-500 group-hover:to-purple-600 transition-all duration-300"
      >
        {{ update.title }}
      </h3>

      <!-- Excerpt -->
      <p class="text-gray-600 text-sm leading-relaxed mb-4 flex-grow">
        {{ update.excerpt }}
      </p>

      <!-- Footer -->
      <div
        class="flex items-center justify-between pt-4 border-t border-gray-100 mt-auto"
      >
        <div class="flex items-center space-x-3">
          <div class="relative">
            <img
              :src="update.authorImage"
              :alt="update.author"
              class="w-10 h-10 rounded-full object-cover ring-2 ring-white shadow-lg"
            />
            <span
              class="absolute bottom-0 right-0 w-3 h-3 bg-green-400 rounded-full border-2 border-white"
            ></span>
          </div>
          <div class="flex flex-col">
            <span class="text-sm font-semibold text-gray-800">{{
              update.author
            }}</span>
            <span class="text-xs text-gray-500">{{
              formatRelativeDate(update.publishDate)
            }}</span>
          </div>
        </div>

        <a
          :href="update.link"
          class="flex items-center space-x-2 px-4 py-2 bg-gradient-to-r from-pink-500 to-purple-600 text-white text-sm font-semibold rounded-xl transition-all duration-300 transform group-hover:translate-x-1 group-hover:shadow-lg"
        >
          <span>Read</span>
          <Icon name="heroicons:arrow-right" class="w-4 h-4" />
        </a>
      </div>
    </div>

    <!-- Hover Border Effect -->
    <div
      class="absolute inset-0 border-2 border-transparent bg-gradient-to-r from-pink-500 to-purple-600 rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 -z-10"
      style="
        padding: 2px;
        mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        -webkit-mask: linear-gradient(#fff 0 0) content-box,
          linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask-composite: exclude;
      "
    ></div>
  </div>
</template>
