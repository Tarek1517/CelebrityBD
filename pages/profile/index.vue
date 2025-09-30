<script setup>
// All Bangladeshi celebrities data
const allCelebrities = [
  {
    id: 1,
    name: "Sakib Khan",
    image: "/images/sakibKhan.jpg",
    category: "Actor",
    profession: "Film Actor",
    followers: "2.5M",
    rating: 4.9,
    projects: 85,
    verified: true,
    featured: true,
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
    verified: true,
    featured: true,
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
    verified: true,
    featured: true,
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
    verified: true,
    featured: false,
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
    verified: true,
    featured: true,
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
    verified: true,
    featured: false,
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
    verified: true,
    featured: true,
  },

  {
    id: 9,
    name: "Moushumi Hamid",
    image: "/images/moushumi.jpg",
    category: "Actress",
    profession: "Film Actress",
    followers: "2.1M",
    rating: 4.7,
    projects: 110,
    verified: true,
    featured: false,
  },
  {
    id: 10,
    name: "Tamim Iqbal",
    image: "/images/tamim.jpg",
    category: "Sports",
    profession: "Cricketer",
    followers: "3.8M",
    rating: 4.6,
    projects: 180,
    verified: true,
    featured: false,
  },
  {
    id: 11,
    name: "Joya Ahsan",
    image: "/images/joya.jpeg",
    category: "Actress",
    profession: "Film Actress",
    followers: "1.9M",
    rating: 4.8,
    projects: 75,
    verified: true,
    featured: false,
  },
  {
    id: 12,
    name: "Fazlur Rahman Babu",
    image: "/images/babu.jpg",
    category: "Actor",
    profession: "Character Actor",
    followers: "850K",
    rating: 4.9,
    projects: 200,
    verified: true,
    featured: false,
  },
];

// Filters and search
const searchQuery = ref("");
const selectedCategory = ref("All");
const sortBy = ref("popular");
const showOnlyVerified = ref(false);
const showOnlyFeatured = ref(false);

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

// Sort options
const sortOptions = [
  { value: "popular", label: "Most Popular" },
  { value: "rating", label: "Highest Rated" },
  { value: "newest", label: "Newest First" },
  { value: "name", label: "Alphabetical" },
];

// Computed filtered celebrities
const filteredCelebrities = computed(() => {
  let filtered = allCelebrities;

  // Search filter
  if (searchQuery.value) {
    filtered = filtered.filter(
      (celeb) =>
        celeb.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        celeb.profession.toLowerCase().includes(searchQuery.value.toLowerCase())
    );
  }

  // Category filter
  if (selectedCategory.value !== "All") {
    filtered = filtered.filter(
      (celeb) => celeb.category === selectedCategory.value
    );
  }

  // Verified filter
  if (showOnlyVerified.value) {
    filtered = filtered.filter((celeb) => celeb.verified);
  }

  // Featured filter
  if (showOnlyFeatured.value) {
    filtered = filtered.filter((celeb) => celeb.featured);
  }

  // Sorting
  switch (sortBy.value) {
    case "popular":
      filtered.sort(
        (a, b) => parseFloat(b.followers) - parseFloat(a.followers)
      );
      break;
    case "rating":
      filtered.sort((a, b) => b.rating - a.rating);
      break;
    case "newest":
      filtered.sort((a, b) => b.id - a.id);
      break;
    case "name":
      filtered.sort((a, b) => a.name.localeCompare(b.name));
      break;
  }

  return filtered;
});

// Pagination
const currentPage = ref(1);
const itemsPerPage = 12;
const totalPages = computed(() =>
  Math.ceil(filteredCelebrities.value.length / itemsPerPage)
);

const paginatedCelebrities = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return filteredCelebrities.value.slice(start, end);
});

// Reset to first page when filters change
watch(
  [searchQuery, selectedCategory, sortBy, showOnlyVerified, showOnlyFeatured],
  () => {
    currentPage.value = 1;
  }
);
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Header Banner -->
    <section
      class="relative h-[550px] bg-cover bg-center bg-no-repeat flex flex-col justify-center text-white py-20 overflow-hidden"
      style="background-image: url('/images/counter.png')"
    >
      <!-- Dark Overlay for better text readability -->
      <div class="absolute inset-0 bg-black/50"></div>

      <!-- Background Pattern -->
      <div class="absolute inset-0 opacity-20">
        <div
          class="absolute top-0 left-0 w-72 h-72 bg-white rounded-full -translate-x-1/2 -translate-y-1/2"
        ></div>
        <div
          class="absolute bottom-0 right-0 w-96 h-96 bg-white rounded-full translate-x-1/3 translate-y-1/3"
        ></div>
      </div>

      <!-- Gradient Overlay -->
      <div
        class="absolute inset-0 bg-gradient-to-r from-primary/35 to-primary/35 mix-blend-overlay"
      ></div>

      <div class="container mx-auto px-6 relative z-10">
        <div class="max-w-4xl mx-auto text-center">
          <div
            class="inline-flex items-center px-6 py-3 bg-white/20 backdrop-blur-sm rounded-full text-sm font-semibold mb-6 border border-white/30"
          >
            <Icon name="heroicons:user-group" class="w-5 h-5 mr-2" />
            Complete Celebrity Directory
          </div>

          <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
            Meet All Bangladeshi
            <span
              class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
              >Celebrities</span
            >
          </h1>

        </div>
      </div>
    </section>

    <!-- Filters Section -->
    <section
      class="pt-20 pb-5 bg-white/80 backdrop-blur-sm z-40"
    >
      <div class="container mx-auto px-6">
        <div
          class="flex flex-col lg:flex-row gap-6 items-start lg:items-center justify-between"
        >
          <!-- Search Bar -->
          <div class="flex-1 w-full lg:max-w-md">
            <div class="relative">
              <Icon
                name="heroicons:magnifying-glass"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <input
                v-model="searchQuery"
                type="text"
                placeholder="Search celebrities by name or profession..."
                class="w-full pl-12 pr-4 py-3 bg-white border border-primary/25 rounded-2xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent shadow-sm"
              />
            </div>
          </div>

          <!-- Filter Controls -->
          <div class="flex flex-wrap gap-4 items-center">
            <!-- Category Filter -->
            <select
              v-model="selectedCategory"
              class="px-4 py-3 bg-white border border-primary/25 rounded-2xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent shadow-sm"
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
              class="px-4 py-3 bg-white border border-primary/25 rounded-2xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent shadow-sm"
            >
              <option
                v-for="option in sortOptions"
                :key="option.value"
                :value="option.value"
              >
                {{ option.label }}
              </option>
            </select>

            <!-- Toggle Filters -->
            <div class="flex items-center space-x-4">
              <label class="flex items-center space-x-2 cursor-pointer">
                <input
                  v-model="showOnlyVerified"
                  type="checkbox"
                  class="rounded border-gray-300 text-primary focus:ring-primary"
                />
                <span class="text-sm font-medium text-gray-700"
                  >Verified Only</span
                >
              </label>
              <label class="flex items-center space-x-2 cursor-pointer">
                <input
                  v-model="showOnlyFeatured"
                  type="checkbox"
                  class="rounded border-gray-300 text-primary focus:ring-primary"
                />
                <span class="text-sm font-medium text-gray-700">Featured</span>
              </label>
            </div>
          </div>
        </div>

        <!-- Active Filters -->
        <div
          v-if="
            searchQuery ||
            selectedCategory !== 'All' ||
            showOnlyVerified ||
            showOnlyFeatured
          "
          class="flex flex-wrap gap-2 mt-4"
        >
          <span class="text-sm text-gray-600">Active filters:</span>
          <button
            v-if="searchQuery"
            @click="searchQuery = ''"
            class="inline-flex items-center px-3 py-1 bg-primary/10 text-primary rounded-full text-sm font-medium hover:bg-primary/20 transition-colors"
          >
            Search: "{{ searchQuery }}"
            <Icon name="heroicons:x-mark" class="w-4 h-4 ml-1" />
          </button>
          <button
            v-if="selectedCategory !== 'All'"
            @click="selectedCategory = 'All'"
            class="inline-flex items-center px-3 py-1 bg-primary/10 text-primary rounded-full text-sm font-medium hover:bg-primary/20 transition-colors"
          >
            Category: {{ selectedCategory }}
            <Icon name="heroicons:x-mark" class="w-4 h-4 ml-1" />
          </button>
          <button
            v-if="showOnlyVerified"
            @click="showOnlyVerified = false"
            class="inline-flex items-center px-3 py-1 bg-primary/10 text-primary rounded-full text-sm font-medium hover:bg-primary/20 transition-colors"
          >
            Verified Only
            <Icon name="heroicons:x-mark" class="w-4 h-4 ml-1" />
          </button>
          <button
            v-if="showOnlyFeatured"
            @click="showOnlyFeatured = false"
            class="inline-flex items-center px-3 py-1 bg-primary/10 text-primary rounded-full text-sm font-medium hover:bg-primary/20 transition-colors"
          >
            Featured
            <Icon name="heroicons:x-mark" class="w-4 h-4 ml-1" />
          </button>
        </div>
      </div>
    </section>

    <!-- Results Section -->
    <section class="">
      <div class="container mx-auto px-6">
        <!-- Results Header -->
        <div
          class="flex flex-col md:flex-row md:items-center md:justify-between mb-8"
        >
          <div>
            <h2 class="text-3xl font-bold text-gray-900 mb-2">
              {{ filteredCelebrities.length }} Celebrities Found
            </h2>
            <p class="text-gray-600">
              Showing {{ paginatedCelebrities.length }} of
              {{ filteredCelebrities.length }} results
            </p>
          </div>

          <!-- View Toggle (Grid/List) -->
          <div class="flex items-center space-x-2 mt-4 md:mt-0">
            <button
              class="p-2 rounded-lg bg-gray-100 text-gray-600 hover:bg-gray-200 transition-colors"
            >
              <Icon name="heroicons:squares-2x2" class="w-5 h-5" />
            </button>
            <button
              class="p-2 rounded-lg bg-primary text-white transition-colors"
            >
              <Icon name="heroicons:list-bullet" class="w-5 h-5" />
            </button>
          </div>
        </div>

        <!-- Celebrities Grid -->
        <div
          v-if="paginatedCelebrities.length > 0"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-12"
        >
          <CelebrityCard
            v-for="celebrity in paginatedCelebrities"
            :key="celebrity.id"
            :celebrity="celebrity"
            class="w-full"
          />
        </div>

        <!-- No Results -->
        <div v-else class="text-center py-16">
          <Icon
            name="heroicons:magnifying-glass"
            class="w-16 h-16 text-gray-400 mx-auto mb-4"
          />
          <h3 class="text-2xl font-bold text-gray-900 mb-2">
            No celebrities found
          </h3>
          <p class="text-gray-600 mb-6">
            Try adjusting your search or filters to find what you're looking
            for.
          </p>
          <button
            @click="
              searchQuery = '';
              selectedCategory = 'All';
              showOnlyVerified = false;
              showOnlyFeatured = false;
            "
            class="px-6 py-3 bg-primary text-white rounded-2xl font-semibold hover:bg-primary/90 transition-colors"
          >
            Clear All Filters
          </button>
        </div>

        <!-- Pagination -->
        <div
          v-if="totalPages > 1"
          class="flex justify-center items-center space-x-2"
        >
          <button
            @click="currentPage--"
            :disabled="currentPage === 1"
            :class="[
              'px-4 py-2 rounded-lg font-semibold transition-colors',
              currentPage === 1
                ? 'bg-gray-100 text-gray-400 cursor-not-allowed'
                : 'bg-white text-gray-700 border border-gray-300 hover:bg-gray-50',
            ]"
          >
            Previous
          </button>

          <div class="flex space-x-1">
            <button
              v-for="page in totalPages"
              :key="page"
              @click="currentPage = page"
              :class="[
                'w-10 h-10 rounded-lg font-semibold transition-colors',
                currentPage === page
                  ? 'bg-primary text-white'
                  : 'bg-white text-gray-700 border border-gray-300 hover:bg-gray-50',
              ]"
            >
              {{ page }}
            </button>
          </div>

          <button
            @click="currentPage++"
            :disabled="currentPage === totalPages"
            :class="[
              'px-4 py-2 rounded-lg font-semibold transition-colors',
              currentPage === totalPages
                ? 'bg-gray-100 text-gray-400 cursor-not-allowed'
                : 'bg-white text-gray-700 border border-gray-300 hover:bg-gray-50',
            ]"
          >
            Next
          </button>
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
