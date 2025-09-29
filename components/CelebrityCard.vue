<script setup>
const props = defineProps({
  celebrity: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <NuxtLink to="/profile/show" class="block group">
    <div
      class="bg-white rounded-2xl shadow-xl overflow-hidden transition-all duration-500 hover:shadow-2xl border border-gray-200/50 h-full flex flex-col hover:-translate-y-2"
    >
      <!-- Image Section with Overlay Content -->
      <div class="relative h-72 overflow-hidden">
        <!-- Celebrity Image -->
        <img
          :src="celebrity.image"
          :alt="celebrity.name"
          class="w-full h-full object-cover object-top transition-transform duration-700 group-hover:scale-110"
          loading="lazy"
        />

        <!-- Gradient Overlay -->
        <div
          class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/20 to-transparent opacity-80 group-hover:opacity-90 transition-opacity duration-500"
        ></div>

        <!-- Top Badges -->
        <div
          class="absolute top-4 left-4 right-4 flex justify-between items-start"
        >
          <span
            class="px-4 py-2 bg-secondary/90 backdrop-blur-sm text-gray-900 text-sm font-semibold rounded-full shadow-lg text-white"
          >
            {{ celebrity.category }}
          </span>
          <div class="flex space-x-2">
            <!-- Share Button -->
            <div class="relative">
              <button
                class="p-2 bg-white/20 backdrop-blur-sm rounded-full shadow-lg hover:bg-white/30 transition-all duration-300 group/share"
              >
                <Icon
                  name="heroicons:share"
                  class="w-5 h-5 text-blue-600 transform group-hover/share:rotate-12 transition-transform"
                />
              </button>

              <!-- Social Share Icons - Appear on hover -->
              <div
                class="absolute top-0 right-full mr-2 flex space-x-2 opacity-0 transform translate-x-4 group-hover/share:opacity-100 group-hover/share:translate-x-0 transition-all duration-300"
              >
                <button
                  class="p-2 bg-blue-500 rounded-full shadow-lg hover:bg-blue-600 transition-colors"
                >
                  <Icon name="mdi:facebook" class="w-4 h-4 text-white" />
                </button>
                <button
                  class="p-2 bg-blue-400 rounded-full shadow-lg hover:bg-blue-500 transition-colors"
                >
                  <Icon name="mdi:twitter" class="w-4 h-4 text-white" />
                </button>
                <button
                  class="p-2 bg-pink-500 rounded-full shadow-lg hover:bg-pink-600 transition-colors"
                >
                  <Icon name="mdi:instagram" class="w-4 h-4 text-white" />
                </button>
              </div>
            </div>

            <!-- Favorite Button -->
            <button
              class="p-2 bg-white/20 backdrop-blur-sm rounded-full shadow-lg hover:bg-red-50 transition-colors"
            >
              <Icon
                name="ic:baseline-favorite"
                class="w-5 h-5 text-rose-600 hover:text-red-500"
              />
            </button>
          </div>
        </div>

        <!-- Bottom Content Overlay -->
        <div class="absolute bottom-0 left-0 right-0 p-6 text-white">
          <h3
            class="text-2xl font-bold mb-2 transform group-hover:translate-y-1 transition-transform duration-300"
          >
            {{ celebrity.name }}
          </h3>
          <p class="text-white/90 text-sm font-medium mb-3">
            {{ celebrity.profession }}
          </p>

          <!-- Stats -->
          <div class="flex items-center space-x-4">
            <div class="flex items-center space-x-2">
              <Icon name="heroicons:user-group" class="w-4 h-4 text-white/80" />
              <span class="text-sm font-semibold">{{
                celebrity.followers
              }}</span>
            </div>
            <div class="flex items-center space-x-2">
              <Icon name="heroicons:map-pin" class="w-4 h-4 text-white/80" />
              <span class="text-sm">Bangladesh</span>
            </div>
          </div>
        </div>

        <!-- Hover Effect Indicator -->
        <div
          class="absolute bottom-4 right-4 w-10 h-10 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center transform translate-y-4 opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-500"
        >
          <Icon name="heroicons:arrow-right" class="w-5 h-5 text-white" />
        </div>
      </div>

      <!-- Content Section -->
      <div class="bg-gradient-to-r from-primary/20 to-secondary/20 p-6 flex-1 flex flex-col">
        <!-- Engagement Metrics -->
        <div class="grid grid-cols-3 gap-4 mb-6">
          <div class="text-center">
            <div class="text-2xl font-bold text-gray-900">150+</div>
            <div class="text-xs text-gray-500 mt-1">Projects</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-gray-900">4.9</div>
            <div class="text-xs text-gray-500 mt-1">Rating</div>
          </div>
          <div class="text-center">
            <div class="text-2xl font-bold text-gray-900">5Y+</div>
            <div class="text-xs text-gray-500 mt-1">Experience</div>
          </div>
        </div>

       <!-- Description -->
        <p class="text-gray-600 text-sm leading-relaxed mb-6 flex-1">
          One of the most prominent {{ celebrity.category.toLowerCase() }} in
          Bangladesh with a massive fan following and remarkable contributions
          to the industry.
        </p>

        <!-- Action Buttons -->
        <div class="flex space-x-3">
          <button
            class="flex-1 bg-gradient-to-r from-primary to-secondary text-white font-semibold py-3 px-4 rounded-xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-lg text-sm"
          >
            View Profile
          </button>
          <button
            class="p-3 border border-primary text-primary rounded-xl hover:bg-primary hover:text-white transition-all duration-300"
          >
            <Icon name="heroicons:envelope" class="w-5 h-5" />
          </button>
        </div>
      </div>
    </div>
  </NuxtLink>
</template>

<style scoped>
/* Custom styles for better visual effects */
.group:hover .group-hover\:scale-110 {
  transform: scale(1.1);
}
</style>
