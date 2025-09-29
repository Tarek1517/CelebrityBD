<script setup>
const celebrityUpdates = [
  {
    id: 1,
    title: "Sakib Khan's New Movie Breaks Box Office Records",
    category: "Film News",
    excerpt:
      "The superstar's latest release earns 10 crore BDT in opening weekend, setting new benchmarks for Bangladeshi cinema.",
    image: "/images/sakibKhan.jpg",
    author: "Film Critic",
    authorImage: "/images/avater1.png",
    link: "/updates/sakib-khan-box-office",
    publishDate: "2024-01-15",
    views: "25K",
    likes: "4.2K",
  },
  {
    id: 3,
    title: "Sabila Nur's Fashion Line Launch Creates Buzz",
    category: "Fashion",
    excerpt:
      "The popular actress ventures into fashion design with her new sustainable clothing collection.",
    image: "/images/sabilanur.jpg",
    author: "Fashion Editor",
    authorImage: "/images/avater1.png",
    link: "/updates/sabila-fashion-line",
    publishDate: "2024-01-10",
    views: "15K",
    likes: "2.9K",
  },
  {
    id: 4,
    title: "Chanchal Chowdhury Wins Best Actor Award",
    category: "Awards",
    excerpt:
      "Veteran actor receives prestigious national award for his outstanding performance in recent drama series.",
    image: "/images/chancal.jpg",
    author: "Entertainment Desk",
    authorImage: "/images/avater1.png",
    link: "/updates/chanchal-award",
    publishDate: "2024-01-08",
    views: "22K",
    likes: "4.5K",
  },
];
</script>

<template>
  <div
    class="w-full pb-20 bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Section Header -->
    <div class="text-center mb-16">
      <div
        class="inline-flex items-center px-6 py-3 bg-gradient-to-r from-pink-500/10 to-purple-500/10 text-pink-600 rounded-full text-sm font-semibold mb-6 shadow-sm border border-pink-200"
      >
        <Icon name="heroicons:newspaper" class="w-5 h-5 mr-2" />
        Celebrity Updates
      </div>

      <h2 class="text-5xl md:text-6xl font-extrabold text-gray-900 mb-6">
        Latest Celebrity
        <span
          class="text-transparent bg-clip-text bg-gradient-to-r from-pink-500 to-purple-600"
          >News & Updates</span
        >
      </h2>
      <p class="text-xl text-gray-600 max-w-3xl mx-auto leading-relaxed">
        Stay updated with the latest news, achievements, and projects from your
        favorite Bangladeshi celebrities.
      </p>
    </div>

    <!-- Updates Grid - Showing exactly 3 cards -->
    <div class="container mx-auto px-6">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <BlogCard
          v-for="update in celebrityUpdates"
          :key="update.id"
          :update="update"
          class="w-full h-[500px]"
        />
      </div>
    </div>

    <!-- View All Button -->
    <div class="text-center mt-12">
      <button
        class="group px-10 py-4 bg-gradient-to-r from-pink-500 to-purple-600 text-white font-bold text-lg rounded-2xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-2xl hover:scale-105"
      >
        <span class="flex items-center justify-center space-x-3">
          <span>View All Updates</span>
          <Icon
            name="heroicons:arrow-right"
            class="w-5 h-5 transform group-hover:translate-x-1 transition-transform"
          />
        </span>
      </button>
    </div>
  </div>
</template>
