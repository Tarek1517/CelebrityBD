<script setup>
const showVideo = ref(false);

const celebrityStats = [
  { title: "Active Celebrities", value: "1.2K", icon: "heroicons:user-group" },
  { title: "Film Industry Stars", value: "850", icon: "heroicons:film" },
  { title: "Sports Personalities", value: "320", icon: "heroicons:trophy" },
  { title: "Social Influencers", value: "2.5K", icon: "heroicons:megaphone" },
];

const trendingCelebrities = [
  { name: "Sakib Khan", category: "Actor", trend: "🔥 #1 Trending" },
  { name: "Shakib Al Hasan", category: "Cricket", trend: "⭐ Most Viewed" },
  { name: "Sabila Nur", category: "Actress", trend: "📈 Rising Star" },
];
</script>

<template>
  <div
    class="w-full"
  >
    <!-- Hero Section -->
    <section
      class="relative min-h-[60vh] flex items-center justify-center bg-cover bg-fixed bg-center text-white overflow-hidden"
      style="
        background-image: linear-gradient(
            rgba(0, 0, 0, 0.6),
            rgba(0, 0, 0, 0.6)
          ),
          url('/images/counter.png');
      "
    >
      <!-- Animated background elements -->
      <div
        class="absolute top-0 left-0 w-full h-full bg-gradient-to-br from-black/15 to-pink-500/10"
      ></div>

      <!-- Floating elements -->
      <div
        class="absolute top-20 left-10 w-6 h-6 rounded-full bg-pink-500/30 animate-float"
      ></div>
      <div
        class="absolute top-40 right-20 w-8 h-8 rounded-full bg-purple-500/40 animate-float animation-delay-1000"
      ></div>
      <div
        class="absolute bottom-32 left-24 w-5 h-5 rounded-full bg-blue-500/30 animate-float animation-delay-2000"
      ></div>

      <div class="container mx-auto px-6 relative z-10">
        <div class="max-w-6xl mx-auto text-center">
          <!-- Video Play Button - Centered -->
          <div class="flex justify-center">
            <!-- Video Modal -->
            <UModal v-model="showVideo" size="4xl" title="Meet Our Celebrities">
              <UButton
                @click="showVideo = true"
                class="group relative w-24 h-24 rounded-full bg-white/10 backdrop-blur-md border-2 border-white/20 flex items-center justify-center shadow-2xl hover:shadow-3xl transition-all duration-500 hover:scale-110 hover:bg-white/20"
              >
                <div
                  class="absolute inset-0 rounded-full bg-white/20 animate-ping group-hover:animate-none"
                ></div>
                <div
                  class="absolute inset-2 rounded-full bg-gradient-to-r from-pink-500 to-purple-600"
                ></div>
                <Icon
                  name="heroicons:play-20-solid"
                  class="text-4xl text-white relative z-10 ml-1 transition-transform group-hover:scale-110"
                />
              </UButton>
              <template #body>
                <div
                  class="aspect-video w-full bg-black rounded-lg overflow-hidden"
                >
                  <iframe
                    v-if="showVideo"
                    class="w-full h-full"
                    src="https://www.youtube.com/embed/dQw4w9WgXcQ?autoplay=1"
                    title="Bangladeshi Celebrities Introduction"
                    frameborder="0"
                    allow="autoplay; encrypted-media"
                    allowfullscreen
                  ></iframe>
                </div>
              </template>
            </UModal>
          </div>

          <!-- Main heading -->
          <h1
            class="text-6xl font-black text-white mb-4 leading-tight"
          >
            Meet Bangladesh's Top
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >Celebraties</span
            >
          
          </h1>

          <!-- Trending Badges -->
          <div class="flex flex-wrap justify-center gap-4 mb-12">
            <div
              v-for="(celeb, index) in trendingCelebrities"
              :key="index"
              class="px-6 py-3 bg-white/10 backdrop-blur-sm rounded-full border border-white/20 hover:bg-white/20 transition-all duration-300 cursor-pointer group"
            >
              <div class="flex items-center space-x-3">
                <span class="text-sm font-semibold text-white">{{
                  celeb.trend
                }}</span>
                <div class="flex items-center space-x-2">
                  <span class="text-white font-bold">{{ celeb.name }}</span>
                  <span
                    class="text-pink-300 text-xs bg-pink-500/20 px-2 py-1 rounded-full"
                  >
                    {{ celeb.category }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="relative -mt-48 overflow-hidden px-6 pb-20">
      <div
        class="container mx-auto px-8 py-16 rounded-3xl relative z-10"
      >
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(stat, index) in celebrityStats"
            :key="index"
            class="group p-8 bg-gradient-to-r from-primary to-secondary backdrop-blur-md rounded-2xl shadow-lg hover:scale-105 transform transition-all duration-500 text-center"
          >
            <!-- Icon -->
            <div class="mb-6">
              <div
                class="w-20 h-20 mx-auto bg-gradient-to-br from-pink-500 to-purple-600 rounded-2xl flex items-center justify-center shadow-2xl group-hover:scale-110 transition-transform duration-300"
              >
                <Icon :name="stat.icon" class="text-4xl text-white" />
              </div>
            </div>

            <!-- Animated counter number -->
            <h3
              class="text-4xl font-black text-white mb-4 tracking-tight"
            >
              {{ stat.value }}+
            </h3>

            <!-- Title -->
            <p class="text-lg font-semibold text-purple-100 tracking-wide">
              {{ stat.title }}
            </p>

            <!-- Progress indicator -->
            <div class="mt-4 w-full bg-white/20 rounded-full h-2">
              <div
                class="h-2 bg-gradient-to-r from-pink-400 to-purple-400 rounded-full transition-all duration-1000"
                :style="{ width: `${70 + index * 10}%` }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style>
.animate-float {
  animation: float 6s ease-in-out infinite;
}

.animation-delay-1000 {
  animation-delay: 1s;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-20px);
  }
}
</style>
