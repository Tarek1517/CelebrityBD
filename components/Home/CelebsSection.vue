<script setup>
// Bangladeshi celebrities data
const celebrities = [
  {
    id: 1,
    name: "Sakib Khan",
    image: "/images/sakibKhan.jpg",
    category: "Actor",
    profession: "Film Actor",
    followers: "2.5M",
    rating: 4.9,
    projects: 85,
    verified: true
  },
  {
    id: 2,
    name: "Shakib Al Hasan",
    image: "/images/ShakibAlHasan.jpeg",
    category: "Sports",
    profession: "Cricketer",
    followers: "8.7M",
    rating: 4.8,
    projects: 250,
    verified: true
  },
  {
    id: 3,
    name: "Chanchal Chowdhury",
    image: "/images/chancal.jpg",
    category: "Actor",
    profession: "Film & TV Actor",
    followers: "1.8M",
    rating: 4.7,
    projects: 120,
    verified: true
  },
  {
    id: 4,
    name: "Dr. Muhammad Yunus",
    image: "/images/drYounus.jpg",
    category: "Social",
    profession: "Nobel Laureate",
    followers: "1.2M",
    rating: 5.0,
    projects: 45,
    verified: true
  },
  {
    id: 5,
    name: "Sabila Nur",
    image: "/images/sabilanur.jpg",
    category: "Actress",
    profession: "Film Actress",
    followers: "3.1M",
    rating: 4.6,
    projects: 65,
    verified: true
  },
  {
    id: 6,
    name: "Puja Cherry",
    image: "/images/pujaCherry.webp",
    category: "Actress",
    profession: "Film Actress",
    followers: "2.9M",
    rating: 4.5,
    projects: 55,
    verified: true
  },
  {
    id: 7,
    name: "Mosharraf Karim",
    image: "/images/mossharrof2.jpg",
    category: "Actor",
    profession: "Film & TV Actor",
    followers: "2.3M",
    rating: 4.8,
    projects: 95,
    verified: true
  },
];

const visibleCelebrities = ref(6);
const showMore = () => {
  visibleCelebrities.value += 3;
  if (visibleCelebrities.value >= celebrities.length) {
    visibleCelebrities.value = celebrities.length;
  }
};

// Filter categories
const categories = ["All", "Actor", "Actress", "Sports", "Social"];
const activeCategory = ref("All");

const filteredCelebrities = computed(() => {
  if (activeCategory.value === "All") {
    return celebrities;
  }
  return celebrities.filter(celeb => celeb.category === activeCategory.value);
});
</script>

<template>
  <section
    class="py-20 bg-gradient-to-br from-slate-50 via-white to-slate-100 relative overflow-hidden"
  >
    <!-- Animated background elements -->
    <div
      class="absolute top-0 right-0 w-96 h-96 bg-gradient-to-r from-blue-500/10 to-purple-500/10 rounded-full -translate-y-1/3 translate-x-1/3 blur-3xl animate-pulse-slow"
    ></div>
    <div
      class="absolute bottom-0 left-0 w-[32rem] h-[32rem] bg-gradient-to-r from-green-500/10 to-cyan-500/10 rounded-full translate-y-1/3 -translate-x-1/3 blur-3xl animate-pulse-slow delay-1000"
    ></div>

    <div class="container mx-auto px-6 relative z-10">
      <!-- Section Header -->
      <div class="text-center mb-10">
        <div
          class="inline-flex items-center px-6 py-3 bg-gradient-to-r from-primary/10 to-secondary/10 text-primary rounded-full text-sm font-semibold mb-3 shadow-sm"
        >
          <Icon name="heroicons:sparkles" class="w-5 h-5 mr-2" />
          Featured Bangladeshi Celebrities
        </div>
        <h2 class="text-5xl md:text-6xl font-bold text-gray-900 mb-6 leading-tight">
          Discover Bangladesh's
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">
            Celebrated Icons
          </span>
        </h2>
        <p class="text-xl text-gray-600 max-w-3xl mx-auto leading-relaxed">
          Meet the most influential and beloved personalities from Bangladesh who are making waves in entertainment, sports, and social impact.
        </p>
      </div>

      <!-- Category Filters -->
      <div class="flex flex-wrap justify-center gap-4 mb-12">
        <button
          v-for="category in categories"
          :key="category"
          @click="activeCategory = category"
          :class="[
            'px-6 py-3 rounded-lg font-semibold transition-all duration-300 transform hover:-translate-y-1',
            activeCategory === category
              ? 'bg-gradient-to-r from-primary to-secondary text-white shadow-lg'
              : 'bg-gray-200 text-gray-700 border border-gray-200 hover:border-primary/30 hover:shadow-md'
          ]"
        >
          {{ category }}
        </button>
      </div>

      <!-- Celebrities Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-8 mb-16">
        <CelebrityCard
          v-for="celebrity in filteredCelebrities.slice(0, visibleCelebrities)"
          :key="celebrity.id"
          :celebrity="celebrity"
          class="w-full"
        />
      </div>

      <!-- Show More Button -->
      <div v-if="visibleCelebrities < filteredCelebrities.length" class="text-center">
        <button
          @click="showMore"
          class="group px-10 py-4 bg-gradient-to-r from-primary to-secondary text-white font-bold text-lg rounded-2xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-2xl hover:scale-105"
        >
          <span class="flex items-center justify-center space-x-3">
            <span>Load More Celebrities</span>
            <Icon name="heroicons:arrow-down" class="w-5 h-5 transform group-hover:translate-y-1 transition-transform" />
          </span>
        </button>
      </div>

      
    </div>
  </section>
</template>

<style>
@keyframes pulse-slow {
  0%, 100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.6;
  }
}

.animate-pulse-slow {
  animation: pulse-slow 6s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>