<!-- components/TrendingCard.vue -->
<script setup>
const props = defineProps({
  celebrity: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <NuxtLink :to="`/celebrities/${celebrity.id}`" class="block group">
    <div
      class="relative bg-white rounded-2xl shadow-xl overflow-hidden transition-all duration-500 border border-gray-200/50 hover:-translate-y-3 h-full"
    >
      <!-- Rank Badge -->
      <div
        class="absolute top-4 left-4 z-20 w-12 h-12 bg-gradient-to-br from-amber-400 to-orange-500 rounded-full flex items-center justify-center text-white font-bold text-lg shadow-2xl border-2 border-white"
      >
        #{{ celebrity.rank }}
      </div>

      <!-- Trend Badge -->
      <div
        class="absolute top-4 right-4 z-20 px-4 py-2 bg-gradient-to-r from-pink-500 to-purple-600 text-white text-xs font-bold rounded-full shadow-lg backdrop-blur-sm"
      >
        {{ celebrity.trend }}
      </div>

      <!-- Celebrity Image -->
      <div class="relative h-72 overflow-hidden">
        <img
          :src="celebrity.image"
          :alt="celebrity.name"
          class="w-full h-full object-cover object-top transition-transform duration-700 group-hover:scale-110"
          loading="lazy"
        />

        <!-- Gradient Overlay -->
        <div
          class="absolute inset-0 bg-gradient-to-t from-black/70 via-black/30 to-transparent opacity-80 group-hover:opacity-90 transition-opacity duration-500"
        ></div>

        <!-- Views Counter -->
        <div
          class="absolute bottom-4 left-4 flex items-center space-x-2 text-white text-sm bg-black/40 backdrop-blur-sm px-3 py-2 rounded-full"
        >
          <Icon name="heroicons:eye" class="w-4 h-4" />
          <span class="font-semibold">{{ celebrity.views }}</span>
        </div>

        <!-- Hover Arrow -->
        <div
          class="absolute bottom-4 right-4 w-10 h-10 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center transform translate-y-4 opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-500"
        >
          <Icon name="heroicons:arrow-right" class="w-5 h-5 text-white" />
        </div>
      </div>

      <!-- Content -->
      <div class="p-6">
        <!-- Name and Category -->
        <div class="mb-4">
          <h3 class="text-2xl font-bold text-gray-900 mb-2 line-clamp-1">
            {{ celebrity.name }}
          </h3>
          <div class="flex items-center justify-between">
            <span
              class="px-3 py-1 bg-gradient-to-r from-blue-500/10 to-cyan-500/10 text-blue-600 text-sm font-semibold rounded-full border border-blue-200"
            >
              {{ celebrity.category }}
            </span>
            <div class="flex items-center space-x-1">
              <div class="flex items-center space-x-1 text-amber-500">
                <Icon name="heroicons:star" class="w-4 h-4" />
                <span class="text-sm font-semibold text-gray-700">4.8</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Circular Progress Bar -->
        <div class="flex items-center justify-between mb-4">
          <div class="flex-1">
            <div class="flex justify-between text-sm text-gray-600 mb-2">
              <span class="font-medium">Popularity</span>
              <span class="font-bold text-green-600">85%</span>
            </div>
            <!-- Modern Progress Bar -->
            <div class="flex items-center justify-between">
              <div class="relative w-16 h-16">
                <!-- Background Circle -->
                <svg class="w-16 h-16 transform -rotate-90" viewBox="0 0 36 36">
                  <!-- Background -->
                  <path
                    d="M18 2.0845
          a 15.9155 15.9155 0 0 1 0 31.831
          a 15.9155 15.9155 0 0 1 0 -31.831"
                    fill="none"
                    stroke="#e2e8f0"
                    stroke-width="3"
                  />
                  <!-- Progress -->
                  <path
                    d="M18 2.0845
          a 15.9155 15.9155 0 0 1 0 31.831
          a 15.9155 15.9155 0 0 1 0 -31.831"
                    fill="none"
                    stroke="url(#gradient)"
                    stroke-width="3"
                    stroke-dasharray="85, 100"
                  />
                  <defs>
                    <linearGradient
                      id="gradient"
                      x1="0%"
                      y1="0%"
                      x2="100%"
                      y2="0%"
                    >
                      <stop offset="0%" stop-color="#10b981" />
                      <stop offset="100%" stop-color="#059669" />
                    </linearGradient>
                  </defs>
                </svg>
                <!-- Percentage Text -->
                <div class="absolute inset-0 flex items-center justify-center">
                  <span class="text-sm font-bold text-gray-900">85%</span>
                </div>
              </div>

              <!-- Chart Info -->
              <div class="flex-1 ml-4">
                <div class="text-sm font-semibold text-gray-900 mb-1">
                  Trend Score
                </div>
                <div class="text-xs text-gray-500">
                  Higher than 92% of celebrities
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Action Button -->
        <button
          class="w-full py-3 bg-gradient-to-r from-primary to-secondary hover:from-secondary hover:to-primary text-white font-semibold rounded-xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-lg text-sm group/btn"
        >
          <span class="flex items-center justify-center space-x-2">
            <span>View Profile</span>
            <Icon
              name="heroicons:arrow-right"
              class="w-4 h-4 transform group-hover/btn:translate-x-1 transition-transform"
            />
          </span>
        </button>
      </div>

      <!-- Hover Glow Effect -->
      <div
        class="absolute inset-0 border-3 border-transparent bg-gradient-to-r from-primary to-secondary rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 -z-10"
        style="
          padding: 3px;
          mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
          -webkit-mask: linear-gradient(#fff 0 0) content-box,
            linear-gradient(#fff 0 0);
          -webkit-mask-composite: xor;
          mask-composite: exclude;
        "
      ></div>
    </div>
  </NuxtLink>
</template>

<style scoped>
.animate-shimmer {
  animation: shimmer 2s infinite;
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}
</style>
