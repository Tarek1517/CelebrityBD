<script setup>
// All trending celebrities data
const trendingCelebrities = [
  {
    id: 1,
    name: "Sakib Khan",
    image: "/images/sakibKhan.jpg",
    category: "Actor",
    trend: "🔥 Hot",
    views: "2.4M",
    rank: 1,
    rating: 4.9,
    trendScore: 95,
    change: "+12%",
    profession: "Film Actor",
    followers: "2.5M",
  },
  {
    id: 2,
    name: "Shakib Al Hasan",
    image: "/images/ShakibAlHasan.jpeg",
    category: "Sports",
    trend: "📈 Rising",
    views: "3.1M",
    rank: 2,
    rating: 4.8,
    trendScore: 88,
    change: "+8%",
    profession: "Cricketer",
    followers: "8.7M",
  },
  {
    id: 3,
    name: "Sabila Nur",
    image: "/images/sabilanur.jpg",
    category: "Actress",
    trend: "⭐ New",
    views: "1.8M",
    rank: 3,
    rating: 4.6,
    trendScore: 85,
    change: "+15%",
    profession: "Film Actress",
    followers: "3.1M",
  },
  {
    id: 4,
    name: "Puja Cherry",
    image: "/images/pujaCherry.webp",
    category: "Actress",
    trend: "💫 Viral",
    views: "2.1M",
    rank: 4,
    rating: 4.5,
    trendScore: 82,
    change: "+22%",
    profession: "Film Actress",
    followers: "2.9M",
  },
  {
    id: 5,
    name: "Chanchal Chowdhury",
    image: "/images/chancal.jpg",
    category: "Actor",
    trend: "🎬 Trending",
    views: "1.5M",
    rank: 5,
    rating: 4.7,
    trendScore: 78,
    change: "+5%",
    profession: "Film & TV Actor",
    followers: "1.8M",
  },
  {
    id: 6,
    name: "Mosharraf Karim",
    image: "/images/mossharrof2.jpg",
    category: "Actor",
    trend: "👑 Popular",
    views: "1.9M",
    rank: 6,
    rating: 4.8,
    trendScore: 75,
    change: "+3%",
    profession: "Film & TV Actor",
    followers: "2.3M",
  },

  {
    id: 8,
    name: "Moushumi",
    image: "/images/moushumi.jpg",
    category: "Actress",
    trend: "🌟 Spotlight",
    views: "1.6M",
    rank: 8,
    rating: 4.7,
    trendScore: 70,
    change: "+7%",
    profession: "Film Actress",
    followers: "2.1M",
  },
  {
    id: 9,
    name: "Joya Ahsan",
    image: "/images/joya.jpg",
    category: "Actress",
    trend: "📊 Growing",
    views: "1.3M",
    rank: 9,
    rating: 4.8,
    trendScore: 68,
    change: "+9%",
    profession: "Film Actress",
    followers: "1.9M",
  },
  {
    id: 10,
    name: "Fazlur Rahman Babu",
    image: "/images/babu.jpg",
    category: "Actor",
    trend: "👍 Steady",
    views: "950K",
    rank: 10,
    rating: 4.9,
    trendScore: 65,
    change: "+2%",
    profession: "Character Actor",
    followers: "850K",
  },
];

// Filters and sorting
const selectedCategory = ref("All");
const selectedTimeframe = ref("weekly");
const sortBy = ref("rank");

// Available categories
const categories = [
  "All",
  "Actor",
  "Actress",
  "Sports",
  "Social",
  "Director",
  "Singer",
];

// Timeframe options
const timeframes = [
  { value: "daily", label: "Today" },
  { value: "weekly", label: "This Week" },
  { value: "monthly", label: "This Month" },
  { value: "alltime", label: "All Time" },
];

// Sort options
const sortOptions = [
  { value: "rank", label: "Trend Rank" },
  { value: "trendScore", label: "Trend Score" },
  { value: "change", label: "Growth Rate" },
  { value: "rating", label: "Rating" },
  { value: "followers", label: "Followers" },
];

// Computed filtered celebrities
const filteredCelebrities = computed(() => {
  let filtered = trendingCelebrities;

  // Category filter
  if (selectedCategory.value !== "All") {
    filtered = filtered.filter(
      (celeb) => celeb.category === selectedCategory.value
    );
  }

  // Sorting
  switch (sortBy.value) {
    case "rank":
      filtered.sort((a, b) => a.rank - b.rank);
      break;
    case "trendScore":
      filtered.sort((a, b) => b.trendScore - a.trendScore);
      break;
    case "change":
      filtered.sort((a, b) => parseFloat(b.change) - parseFloat(a.change));
      break;
    case "rating":
      filtered.sort((a, b) => b.rating - a.rating);
      break;
    case "followers":
      filtered.sort(
        (a, b) => parseFloat(b.followers) - parseFloat(a.followers)
      );
      break;
  }

  return filtered;
});
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Header Banner -->
    <section
      class="relative h-[550px] bg-cover bg-center bg-no-repeat flex flex-col justify-center text-white py-20 overflow-hidden"
      style="background-image: url('/images/counter3.png')"
    >
      <div class="absolute inset-0 bg-black/50"></div>
      <!-- Background Pattern -->
      <div class="absolute inset-0 opacity-10">
        <div
          class="absolute top-0 left-0 w-72 h-72 bg-white rounded-full -translate-x-1/2 -translate-y-1/2"
        ></div>
        <div
          class="absolute bottom-0 right-0 w-96 h-96 bg-white rounded-full translate-x-1/3 translate-y-1/3"
        ></div>
      </div>

      <div class="container mx-auto px-6 relative z-10">
        <div class="max-w-4xl mx-auto text-center">
          <div
            class="inline-flex items-center px-6 py-3 bg-white/20 backdrop-blur-sm rounded-full text-sm font-semibold mb-6 border border-white/30"
          >
            <Icon name="ic:baseline-trending-up" class="w-5 h-5 mr-2" />
            Live Trending Rankings
          </div>

          <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
            Trending
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >Celebrities</span
            >
          </h1>

          <p class="text-xl md:text-2xl text-white/90 mb-8 leading-relaxed">
            Discover who's making waves in Bangladesh right now. Real-time
            rankings based on social engagement, media mentions, and fan
            interactions.
          </p>

          <!-- Quick Stats -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-12">
            <div class="text-center">
              <div
                class="text-3xl md:text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >
                {{ trendingCelebrities.length }}+
              </div>
              <div class="text-white/80">Trending Stars</div>
            </div>
            <div class="text-center">
              <div
                class="text-3xl md:text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >
                25M+
              </div>
              <div class="text-white/80">Daily Views</div>
            </div>
            <div class="text-center">
              <div
                class="text-3xl md:text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >
                4.8
              </div>
              <div class="text-white/80">Avg Rating</div>
            </div>
            <div class="text-center">
              <div
                class="text-3xl md:text-4xl font-black text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >
                Updated
              </div>
              <div class="text-white/80">Just Now</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Filters Section -->
    <section
      class="py-8 bg-white/80 backdrop-blur-sm border-b border-gray-200 top-0 z-40"
    >
      <div class="container mx-auto px-6">
        <div
          class="flex flex-col lg:flex-row gap-6 items-start lg:items-center justify-between"
        >
          <!-- Timeframe Filter -->
          <div class="flex items-center space-x-4">
            <span class="text-sm font-medium text-gray-700">Timeframe:</span>
            <div class="flex bg-gray-100 rounded-lg p-1">
              <button
                v-for="timeframe in timeframes"
                :key="timeframe.value"
                @click="selectedTimeframe = timeframe.value"
                :class="[
                  'px-4 py-2 rounded-md text-sm font-medium transition-all duration-200',
                  selectedTimeframe === timeframe.value
                    ? 'bg-white text-primary shadow-sm'
                    : 'text-gray-600 hover:text-gray-900',
                ]"
              >
                {{ timeframe.label }}
              </button>
            </div>
          </div>

          <!-- Category & Sort Filters -->
          <div class="flex flex-wrap gap-4 items-center">
            <!-- Category Filter -->
            <select
              v-model="selectedCategory"
              class="px-4 py-2 bg-white border border-primary/35 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent shadow-sm"
            >
              <option value="All">All Categories</option>
              <option
                v-for="category in categories.filter((c) => c !== 'All')"
                :key="category"
                :value="category"
              >
                {{ category }}
              </option>
            </select>

            <!-- Sort By -->
            <select
              v-model="sortBy"
              class="px-4 py-2 bg-white border border-primary/35 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent shadow-sm"
            >
              <option
                v-for="option in sortOptions"
                :key="option.value"
                :value="option.value"
              >
                Sort by: {{ option.label }}
              </option>
            </select>
          </div>
        </div>
      </div>
    </section>

    <!-- Trending List Section -->
    <section class="py-12">
      <div class="container mx-auto px-6">
        <!-- Results Header -->
        <div
          class="flex flex-col md:flex-row md:items-center md:justify-between mb-8"
        >
          <div>
            <h2 class="text-3xl font-bold text-gray-900 mb-2">
              Trending Rankings
            </h2>
            <p class="text-gray-600">
              {{ filteredCelebrities.length }} celebrities trending
              {{
                timeframes
                  .find((t) => t.value === selectedTimeframe)
                  ?.label.toLowerCase()
              }}
            </p>
          </div>

          <!-- View Options -->
          <div class="flex items-center space-x-4 mt-4 md:mt-0">
            <span class="text-sm text-gray-600">Last updated: 5 min ago</span>
          </div>
        </div>

        <!-- Trending Grid using TrendingCard Component -->
        <div
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"
        >
          <TrendingCard
            v-for="celebrity in filteredCelebrities"
            :key="celebrity.id"
            :celebrity="celebrity"
            class="w-full"
          />
        </div>

        <!-- Load More -->
        <div class="text-center mt-12">
          <button
            class="group px-8 py-3 bg-white border border-primary/55 text-primary font-semibold rounded-xl hover:border-primary hover:text-primary transition-all duration-300 transform hover:-translate-y-1"
          >
            <span class="flex items-center justify-center space-x-2">
              <span>Load More Trending</span>
              <Icon
                name="heroicons:arrow-down"
                class="w-4 h-4 transform group-hover:translate-y-1 transition-transform"
              />
            </span>
          </button>
        </div>
      </div>
    </section>

    <!-- Trending Insights Section -->
    <section class="py-16 bg-gradient-to-r from-primary/5 to-secondary/5">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold text-gray-900 mb-4">
            Trending Insights
          </h2>
          <p class="text-xl text-gray-600 max-w-2xl mx-auto">
            Understand what's driving the trends in Bangladeshi celebrity
            culture
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div
            class="bg-white rounded-2xl p-6 shadow-lg border border-primary/35"
          >
            <div
              class="w-12 h-12 bg-gradient-to-r from-primary to-secondary rounded-xl flex items-center justify-center mb-4"
            >
              <Icon name="heroicons:chart-bar" class="w-6 h-6 text-white" />
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-2">
              Social Media Buzz
            </h3>
            <p class="text-gray-600">
              Real-time tracking of mentions, shares, and engagement across all
              major platforms.
            </p>
          </div>

          <div
            class="bg-white rounded-2xl p-6 shadow-lg border border-primary/35"
          >
            <div
              class="w-12 h-12 bg-gradient-to-r from-primary to-secondary rounded-xl flex items-center justify-center mb-4"
            >
              <Icon name="heroicons:newspaper" class="w-6 h-6 text-white" />
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-2">Media Coverage</h3>
            <p class="text-gray-600">
              Monitoring news articles, interviews, and features in leading
              publications.
            </p>
          </div>

          <div
            class="bg-white rounded-2xl p-6 shadow-lg border border-primary/35"
          >
            <div
              class="w-12 h-12 bg-gradient-to-r from-primary to-secondary rounded-xl flex items-center justify-center mb-4"
            >
              <Icon name="heroicons:user-group" class="w-6 h-6 text-white" />
            </div>
            <h3 class="text-xl font-bold text-gray-900 mb-2">Fan Engagement</h3>
            <p class="text-gray-600">
              Analyzing fan interactions, comments, and community growth
              patterns.
            </p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.sticky {
  position: sticky;
}
</style>
