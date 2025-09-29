<script setup>
const trendingCelebrities = [
  {
    id: 1,
    name: "Sakib Khan",
    image: "/images/sakibKhan.jpg",
    category: "Actor",
    trend: "🔥 Hot",
    views: "2.4M",
    rank: 1,
  },
  {
    id: 2,
    name: "Shakib Al Hasan",
    image: "/images/ShakibAlHasan.jpeg",
    category: "Sports",
    trend: "📈 Rising",
    views: "3.1M",
    rank: 2,
  },
  {
    id: 3,
    name: "Sabila Nur",
    image: "/images/sabilanur.jpg",
    category: "Actress",
    trend: "⭐ New",
    views: "1.8M",
    rank: 3,
  },
  {
    id: 4,
    name: "Puja Cherry",
    image: "/images/pujaCherry.webp",
    category: "Actress",
    trend: "💫 Viral",
    views: "2.1M",
    rank: 4,
  },
  {
    id: 5,
    name: "Chanchal Chowdhury",
    image: "/images/chancal.jpg",
    category: "Actor",
    trend: "🎬 Trending",
    views: "1.5M",
    rank: 5,
  },
  {
    id: 6,
    name: "Mosharraf Karim",
    image: "/images/mossharrof2.jpg",
    category: "Actor",
    trend: "👑 Popular",
    views: "1.9M",
    rank: 6,
  },
];
</script>

<template>
  <div
    class="w-full py-20 bg-gradient-to-br from-slate-50 via-white to-slate-100 relative overflow-hidden"
  >
    <!-- Section Header -->
    <div class="text-center mb-16 relative z-10">
      
      <h2 class="text-5xl md:text-6xl font-extrabold text-gray-900 mb-6">
        This Week's
        <span
          class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
          >Trending Stars</span
        >
      </h2>
      <p class="text-xl text-gray-600 max-w-3xl mx-auto leading-relaxed">
        Discover the most talked-about Bangladeshi celebrities making waves this
        week. Stay updated with who's trending in entertainment and sports.
      </p>
    </div>

    <!-- Trending Celebrities Carousel -->
    <div class="container mx-auto px-3 relative z-10">
      <UCarousel
        :items="trendingCelebrities"
        loop
        auto-scroll
        :autoplay="{ delay: 3000 }"
        :slides-per-view="4"
        :slide-to-scroll="1"
        class="overflow-visible"
        :ui="{ item: 'basis-full sm:basis-1/2 lg:basis-1/4 ' }"
        arrows
        dots
      >
        <template #default="{ item: celebrity }">
          <TrendingCard :celebrity="celebrity" />
        </template>
      </UCarousel>
    </div>

    <!-- View All Trending Button -->
    <div class="text-center mt-12 relative z-10">
      <button
        class="group px-10 py-4 bg-gradient-to-r from-primary to-secondary hover:from-secondary hover:to-primary text-white font-bold text-lg rounded-2xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-2xl hover:scale-105"
      >
        <span class="flex items-center justify-center space-x-3">
          <span>View All Trending</span>
          <Icon
            name="heroicons:arrow-right"
            class="w-5 h-5 transform group-hover:translate-x-1 transition-transform"
          />
        </span>
      </button>
    </div>
  </div>
</template>

<style scoped>
.animate-pulse-slow {
  animation: pulse-slow 6s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse-slow {
  0%,
  100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.6;
  }
}
</style>
