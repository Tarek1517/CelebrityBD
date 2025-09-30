<script setup>
const celebrityBlogs = [
  {
    id: 1,
    title: "Sakib Khan's New Movie Breaks Box Office Records",
    category: "Film News",
    excerpt:
      "The superstar's latest release earns 10 crore BDT in opening weekend, setting new benchmarks for Bangladeshi cinema.",
    image: "/images/taandob.jpg",
    author: "Film Critic",
    authorImage: "/images/avater1.png",
    link: "/updates/sakib-khan-box-office",
    publishDate: "2024-01-15",
    views: "25K",
    likes: "4.2K",
  },
  {
    id: 2,
    title: "Shakib Al Hasan's Comeback: What to Expect",
    category: "Sports Update",
    excerpt:
      "After recovering from injury, the cricket legend shares his plans for the upcoming international season.",
    image: "/images/ShakibAlHasan.jpeg",
    author: "Sports Analyst",
    authorImage: "/images/avater1.png",
    link: "/updates/shakib-comeback",
    publishDate: "2024-01-12",
    views: "18K",
    likes: "3.8K",
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
  {
    id: 5,
    title: "Puja Cherry's Social Initiative Goes Viral",
    category: "Social Work",
    excerpt:
      "Actress launches education fund for underprivileged children, receives overwhelming public support.",
    image: "/images/pujaCherry.webp",
    author: "Social Reporter",
    authorImage: "/images/avater1.png",
    link: "/updates/puja-social-initiative",
    publishDate: "2024-01-05",
    views: "30K",
    likes: "5.1K",
  },
  {
    id: 6,
    title: "Mosharraf Karim's Comedy Special Breaks Records",
    category: "Entertainment",
    excerpt:
      "The beloved comedian's latest show attracts record audience and critical acclaim nationwide.",
    image: "/images/mossharrof2.jpg",
    author: "Comedy Critic",
    authorImage: "/images/avater1.png",
    link: "/updates/mosharraf-comedy-special",
    publishDate: "2024-01-03",
    views: "28K",
    likes: "4.8K",
  },
];

const latestBlogs = [
  {
    id: 7,
    slug: "latest-blog-post",
    title: "Latest Blog Post",
    blog_image_url:
      "https://images.unsplash.com/photo-1542435503-956c469947f6?ixlib=rb-4.0.3&auto=format&fit=crop&w=1074&q=80",
    publish_date: "2025-09-10",
    blog_reviews: [{ rating: 5 }, { rating: 5 }, { rating: 4 }],
  },
];

const topArticles = [
  {
    id: 8,
    slug: "top-article",
    title: "Top Article Sample",
    blog_image_url:
      "https://images.unsplash.com/photo-1492724441997-5dc865305da7?ixlib=rb-4.0.3&auto=format&fit=crop&w=1172&q=80",
    publish_date: "2025-08-28",
    blog_reviews: [],
  },
  {
    id: 9,
    slug: "second-top-article",
    title: "Second Top Article",
    blog_image_url:
      "https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=1170&q=80",
    publish_date: "2025-08-20",
    blog_reviews: [{ rating: 4 }],
  },
];

// ✅ Utility
const formatDate = (dateStr) => {
  if (!dateStr) return "";
  const date = new Date(dateStr);
  return date.toLocaleDateString("en-US", {
    year: "numeric",
    month: "long",
    day: "numeric",
  });
};
</script>

<template>
  <!-- Header Banner -->
  <section
    class="relative h-[550px] bg-cover bg-center bg-no-repeat flex flex-col justify-center text-white py-20 overflow-hidden"
    style="background-image: url('/images/blog.png')"
  >
    <!-- Dark Overlay for better text readability -->
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
          <Icon name="heroicons:newspaper" class="w-5 h-5 mr-2" />
          Celebrity News & Updates
        </div>

        <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
          Latest
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">Celebrity News</span>
        </h1>

        <p class="text-xl md:text-2xl text-white/90 mb-8 leading-relaxed">
          Stay updated with the latest news, achievements, and exclusive stories
          from your favorite Bangladeshi celebrities.
        </p>
      </div>
    </div>
  </section>

  <!-- Blog Content Section -->
  <section class="container mx-auto px-6 py-20">
    <div class="flex flex-wrap lg:py-5">
      <!-- Blog Posts Section -->
      <div class="w-full lg:w-3/4 rounded-lg px-4">
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <BlogCard
            v-for="update in celebrityBlogs"
            :key="update.id"
            :update="update"
          />
        </div>

        <!-- Load More Button -->
        <div class="text-center mt-12">
          <button
            class="group px-10 py-4 bg-gradient-to-r from-primary to-secondary text-white font-bold text-lg rounded-2xl transition-all duration-300 transform hover:-translate-y-1 hover:shadow-2xl hover:scale-105"
          >
            <span class="flex items-center justify-center space-x-3">
              <span>Load More Articles</span>
              <Icon
                name="heroicons:arrow-down"
                class="w-5 h-5 transform group-hover:translate-y-1 transition-transform"
              />
            </span>
          </button>
        </div>
      </div>

      <!-- Sidebar Section -->
      <div class="w-full lg:w-1/4 lg:pb-10 mt-12 lg:mt-0">
        <!-- Top Articles -->
        <div
          class="bg-gradient-to-br from-gray-50 to-white p-6 rounded-2xl shadow-lg border border-primary/25 mb-8"
        >
          <h2
            class="text-2xl font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200 flex items-center gap-2"
          >
            <Icon name="mdi:fire" class="text-orange-500" />
            Top Articles
          </h2>

          <div
            v-for="blogs in topArticles"
            :key="blogs.id"
            class="w-full my-5 flex items-center gap-4 group/item hover:bg-gray-50 p-3 rounded-xl transition-colors duration-300"
          >
            <div
              class="relative overflow-hidden rounded-lg w-20 h-16 flex-shrink-0"
            >
              <img
                class="w-full h-full object-cover group-hover/item:scale-110 transition-transform duration-500"
                :src="blogs?.blog_image_url"
                alt="Blog Image"
              />
              <div
                class="absolute inset-0 bg-black/20 opacity-0 group-hover/item:opacity-100 transition-opacity duration-300"
              ></div>
            </div>
            <div class="flex-1 min-w-0">
              <p
                class="text-sm font-semibold text-gray-900 leading-tight mb-2 line-clamp-2 group-hover/item:text-primary transition-colors duration-300"
              >
                <NuxtLink :to="`/blog-details/${blogs?.slug}`">
                  {{ blogs?.title }}
                </NuxtLink>
              </p>

              <div class="flex items-center text-xs text-gray-600 gap-3">
                <span class="flex items-center gap-1">
                  <Icon name="mdi:calendar" class="w-3 h-3" />
                  {{ formatDate(blogs?.publish_date) }}
                </span>
                <span class="flex items-center gap-1">
                  <Icon name="mdi:star" class="w-3 h-3 text-yellow-500" />
                  {{
                    blogs?.blog_reviews.length > 0
                      ? `${blogs?.blog_reviews.length} review${
                          blogs?.blog_reviews.length > 1 ? "s" : ""
                        }`
                      : "No reviews"
                  }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- Latest Articles -->
        <div
          class="bg-gradient-to-br from-gray-50 to-white p-6 rounded-2xl shadow-lg border border-primary/25"
        >
          <h2
            class="text-2xl font-bold text-gray-900 mb-6 pb-3 border-b border-gray-200 flex items-center gap-2"
          >
            <Icon name="mdi:clock-outline" class="text-blue-500" />
            Latest Articles
          </h2>

          <div
            v-for="blogs in latestBlogs"
            :key="blogs.id"
            class="w-full my-5 flex items-center gap-4 group/item hover:bg-gray-50 p-3 rounded-xl transition-colors duration-300"
          >
            <div
              class="relative overflow-hidden rounded-lg w-20 h-16 flex-shrink-0"
            >
              <img
                class="w-full h-full object-cover group-hover/item:scale-110 transition-transform duration-500"
                :src="blogs?.blog_image_url"
                alt="Blog Image"
              />
              <div
                class="absolute inset-0 bg-black/20 opacity-0 group-hover/item:opacity-100 transition-opacity duration-300"
              ></div>
            </div>
            <div class="flex-1 min-w-0">
              <p
                class="text-sm font-semibold text-gray-900 leading-tight mb-2 line-clamp-2 group-hover/item:text-primary transition-colors duration-300"
              >
                <NuxtLink :to="`/blog-details/${blogs?.slug}`">
                  {{ blogs?.title }}
                </NuxtLink>
              </p>

              <div class="flex items-center text-xs text-gray-600 gap-3">
                <span class="flex items-center gap-1">
                  <Icon name="mdi:calendar" class="w-3 h-3" />
                  {{ formatDate(blogs?.publish_date) }}
                </span>
                <span class="flex items-center gap-1">
                  <Icon name="mdi:star" class="w-3 h-3 text-yellow-500" />
                  {{
                    blogs?.blog_reviews.length > 0
                      ? `${blogs?.blog_reviews.length} review${
                          blogs?.blog_reviews.length > 1 ? "s" : ""
                        }`
                      : "No reviews"
                  }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <!-- Newsletter Subscription -->
        <div
          class="bg-gradient-to-r from-primary to-secondary p-6 rounded-2xl shadow-lg mt-8"
        >
          <h3 class="text-xl font-bold text-white mb-3">Stay Updated</h3>
          <p class="text-white/90 text-sm mb-4">
            Get the latest celebrity news delivered to your inbox.
          </p>
          <div class="flex space-x-2">
            <input
              type="email"
              placeholder="Your email"
              class="flex-1 px-3 py-2 bg-white rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-white"
            />
            <button
              class="px-4 py-2 bg-white text-primary font-semibold rounded-lg hover:bg-gray-100 transition-colors text-sm"
            >
              Subscribe
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
