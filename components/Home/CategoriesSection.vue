<script setup lang="ts">
// Define celebrity categories with counts
const items = [
  { title: "Movie Stars", icon: "mdi:movie", count: "1.2K" },
  { title: "Musicians", icon: "mdi:music", count: "856" },
  { title: "YouTubers", icon: "mdi:youtube", count: "2.4K" },
  { title: "Sports Stars", icon: "mdi:trophy", count: "742" },
  { title: "Influencers", icon: "mdi:instagram", count: "3.1K" },
  { title: "Bloggers", icon: "mdi:pen", count: "1.8K" },
];
</script>

<template>
  <section
    class="w-full relative overflow-hidden py-20 bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Animated background elements -->
    <div
      class="absolute top-0 right-0 w-96 h-96 bg-gradient-to-r from-blue-500/10 to-purple-500/10 rounded-full -translate-y-1/3 translate-x-1/3 blur-3xl animate-pulse-slow"
    ></div>
    <div
      class="absolute bottom-0 left-0 w-[32rem] h-[32rem] bg-gradient-to-r from-green-500/10 to-cyan-500/10 rounded-full translate-y-1/3 -translate-x-1/3 blur-3xl animate-pulse-slow delay-1000"
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <!-- Heading -->
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">
          Explore Top
          <span
            class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
          >
            Celebrity Categories
          </span>
        </h2>
        <p class="text-gray-600 text-lg max-w-2xl mx-auto">
          Discover thousands of celebrities across different categories and
          connect with your favorites.
        </p>
      </div>

      <!-- Carousel Container -->
      <div class="relative">
        <UCarousel
          v-slot="{ item }"
          loop
          dots
          arrows
          auto-scroll
          :items="items"
          :ui="{
            item: 'basis-full sm:basis-1/2 lg:basis-1/4 min-w-0',
            container: 'overflow-visible',
          }"
        >
          <div
            class="group bg-white/80 backdrop-blur-sm rounded-2xl p-6 transition-all border border-primary duration-500 relative overflow-hidden h-full"
          >
            <!-- Corner accent -->
            <div
              class="absolute top-0 right-0 w-20 h-20 bg-gradient-to-bl from-blue-500/10 to-purple-500/10 rounded-bl-3xl transition-all duration-500 group-hover:from-blue-500/20 group-hover:to-purple-500/20"
            ></div>

            <!-- Icon Container -->
            <div class="relative z-10 mb-3">
              <div
                class="w-16 h-16 bg-gradient-to-br from-primary to-secondary rounded-2xl flex items-center justify-center shadow-lg group-hover:shadow-xl transition-all duration-500 group-hover:scale-110"
              >
                <Icon :name="item.icon" class="text-3xl text-white" />
              </div>
            </div>

            <!-- Content -->
            <div class="relative z-10">
              <h3
                class="font-bold text-xl text-gray-900 mb-2 group-hover:text-gray-800 transition-colors"
              >
                {{ item.title }}
              </h3>

              <div class="flex items-center mb-3">
                <div
                  class="w-3 h-3 bg-green-500 rounded-full mr-3 animate-pulse shadow-lg"
                ></div>
                <span class="text-lg font-semibold text-gray-700"
                  >{{ item.count }} Celebrities</span
                >
              </div>

              <p class="text-gray-600 text-sm leading-relaxed mb-6">
                Discover talented {{ item.title.toLowerCase() }} and connect
                with your favorite personalities.
              </p>
            </div>

            <!-- Action Button -->
            <div class="relative z-10">
              <button
                class="group/btn w-full py-2 bg-gradient-to-r border border-primary/15 from-primary to-secondary hover:from-secondary hover:to-primary rounded-xl text-white font-medium transition-all duration-500 shadow-md hover:shadow-xl transform hover:-translate-y-1"
              >
                <span class="flex items-center justify-center space-x-2">
                  <span>Explore</span>
                  <Icon
                    name="mdi:arrow-right"
                    class="w-5 h-5 transform group-hover/btn:translate-x-1 transition-transform duration-300"
                  />
                </span>
              </button>
            </div>
          </div>
        </UCarousel>
      </div>
    </div>
  </section>
</template>

<style>
@keyframes pulse-slow {
  0%,
  100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.6;
  }
}

.animate-pulse-slow {
  animation: pulse-slow 6s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

/* Custom carousel styles */
.carousel-item {
  flex: 0 0 25%;
  min-width: 0;
}

@media (max-width: 1024px) {
  .carousel-item {
    flex: 0 0 50%;
  }
}

@media (max-width: 640px) {
  .carousel-item {
    flex: 0 0 100%;
  }
}
</style>
