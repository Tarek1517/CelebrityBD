<script setup>
// ✅ Static Blog Details - Sakib Khan News
const BlogDetails = {
  id: 1,
  slug: "sakib-khan-tandob-movie-success",
  title: "Sakib Khan's 'Tandob' Creates History at Box Office",
  blog_image_url: "/images/taandob.jpg",
  publish_date: "2024-01-15",
  short_description:
    "Sakib Khan's latest action thriller 'Tandob' breaks all previous records, earning 15 crore BDT in opening weekend.",
  description: `
    <p>Bangladeshi superstar Sakib Khan has once again proven his box office dominance with his latest release "Tandob." The action-packed thriller has taken the industry by storm, setting new benchmarks for Bangladeshi cinema.</p>
    
    <h3>Record-Breaking Opening</h3>
    <p>"Tandob" opened to packed houses across the country, with fans queuing up hours before showtimes. The film earned an unprecedented 15 crore BDT in its opening weekend, making it the highest-grossing opening in Bangladeshi cinema history.</p>
    
    <p>The movie's success has been attributed to Sakib Khan's powerful performance, stunning action sequences, and engaging storyline that has resonated with audiences of all ages.</p>
    
    <h3>Critical Acclaim</h3>
    <p>Critics have praised Sakib Khan's versatility in portraying a complex character. His transformation from a romantic hero to an action star has been particularly well-received by both fans and industry experts.</p>
    
    <p>Director Raj Chakraborty expressed his excitement about the film's success: "Working with Sakib is always a pleasure. His dedication to his craft and connection with the audience is what makes him the superstar he is today."</p>
    
    <h3>Fan Reactions</h3>
    <p>Social media has been buzzing with positive reactions from fans. Many have called it Sakib Khan's career-best performance, while others are already demanding a sequel.</p>
    
    <p>The film's success has also boosted the entire Bangladeshi film industry, with increased footfall in cinemas and renewed interest in local productions.</p>
  `,
  blog_reviews: [
    {
      id: 1,
      name: "Film Critic",
      rating: 5,
      reviewMassage:
        "Sakib Khan delivers a powerhouse performance in Tandob. This film sets a new standard for action cinema in Bangladesh. The stunts are breathtaking and the emotional depth is remarkable.",
      status: "publish",
      created_at: "2024-01-16",
      avatar: "/images/avater1.png",
    },
    {
      id: 2,
      name: "Movie Enthusiast",
      rating: 4,
      reviewMassage:
        "Absolutely loved the film! Sakib Khan's action sequences are world-class. The storyline keeps you engaged throughout. A must-watch for all Bangladeshi cinema lovers.",
      status: "publish",
      created_at: "2024-01-15",
      avatar: "/images/avater1.png",
    },
    {
      id: 3,
      name: "Cinema Lover",
      rating: 5,
      reviewMassage:
        "This is why Sakib Khan is called the king of Bangladeshi cinema. Tandob proves that local films can compete with international productions in terms of quality and entertainment.",
      status: "publish",
      created_at: "2024-01-14",
      avatar: "/images/avater1.png",
    },
  ],
};

// ✅ Static Latest Blogs - Celebrity News
const latestBlogs = [
  {
    id: 2,
    slug: "shakib-al-hasan-comeback",
    title: "Shakib Al Hasan Returns to International Cricket",
    blog_image_url: "/images/ShakibAlHasan.jpeg",
    publish_date: "2024-01-12",
    blog_reviews: [{ rating: 4 }, { rating: 5 }],
  },
  {
    id: 3,
    slug: "sabila-nur-fashion-line",
    title: "Sabila Nur Launches Sustainable Fashion Brand",
    blog_image_url: "/images/sabilanur.jpg",
    publish_date: "2024-01-10",
    blog_reviews: [],
  },
  {
    id: 4,
    slug: "chanchal-chowdhury-award",
    title: "Chanchal Chowdhury Wins National Film Award",
    blog_image_url: "/images/chancal.jpg",
    publish_date: "2024-01-08",
    blog_reviews: [{ rating: 5 }],
  },
];

// ✅ Static Top Articles - Celebrity News
const topArticles = [
  {
    id: 5,
    slug: "puja-cherry-social-work",
    title: "Puja Cherry's Charity Initiative Impacts Thousands",
    blog_image_url: "/images/pujaCherry.webp",
    publish_date: "2024-01-05",
    blog_reviews: [{ rating: 5 }],
  },
  {
    id: 6,
    slug: "mosharraf-karim-comedy",
    title: "Mosharraf Karim's Comedy Special Breaks Records",
    blog_image_url: "/images/mossharrof2.jpg",
    publish_date: "2024-01-03",
    blog_reviews: [{ rating: 4 }, { rating: 5 }],
  },
  {
    id: 7,
    slug: "bobby-new-movie",
    title: "Bobby Starts Shooting for New Romantic Drama",
    blog_image_url: "/images/moushumi.jpg",
    publish_date: "2024-01-01",
    blog_reviews: [{ rating: 4 }],
  },
];

// ✅ Reviews form state
import { ref, computed } from "vue";
const rating = ref(0);
const review = ref({
  rating: 0,
  reviewMassage: "",
  name: "",
  email: "",
  blog_slug: BlogDetails.slug,
});

// ✅ Submit handler (static simulation)
const onSubmit = () => {
  if (
    !review.value.name ||
    !review.value.email ||
    !review.value.reviewMassage
  ) {
    alert("Please fill in all fields!");
    return;
  }
  alert("Review submitted successfully! (Simulated)");
  review.value = {
    rating: 0,
    reviewMassage: "",
    name: "",
    email: "",
    blog_slug: BlogDetails.slug,
  };
  rating.value = 0;
};

// ✅ Compute average rating
const averageRating = computed(() => {
  const reviews = BlogDetails.blog_reviews;
  if (reviews.length === 0) return 0;
  const total = reviews.reduce((sum, r) => sum + parseInt(r.rating), 0);
  return Math.round(total / reviews.length);
});

// ✅ Date formatting
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
    class="relative h-[550px] bg-cover bg-top bg-no-repeat flex flex-col justify-center text-white py-20 overflow-hidden"
    style="background-image: url('/images/Taandob-banner.webp')"
  >
    <!-- Dark Overlay for better text readability -->
    <div class="absolute inset-0 bg-black/40"></div>
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
      <div class="max-w-7xl mx-auto text-center">
        <div
          class="inline-flex items-center px-6 py-3 bg-white/20 backdrop-blur-sm rounded-full text-sm font-semibold mb-6 border border-white/30"
        >
          <Icon name="heroicons:newspaper" class="w-5 h-5 mr-2" />
          Exclusive Celebrity News
        </div>

        <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
          {{ BlogDetails.title }}
        </h1>

        <p class="text-xl md:text-2xl text-white/90 mb-8 leading-relaxed">
          Breaking records and setting new standards in Bangladeshi cinema with
          the blockbuster movie "Tandob"
        </p>
      </div>
    </div>
  </section>

  <!-- Blog Content -->
  <section class="container mx-auto px-6 my-20">
    <div class="flex flex-col lg:flex-row gap-10">
      <!-- Main Blog Content - Left Column -->
      <div class="w-full lg:w-2/3">
        <div
          class="bg-white rounded-3xl shadow-2xl border border-gray-200 overflow-hidden"
        >
          <!-- Featured Image -->
          <div class="relative h-96 overflow-hidden">
            <img
              :src="BlogDetails.blog_image_url"
              alt="Sakib Khan in Tandob"
              class="w-full h-full object-cover"
            />
            <div
              class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"
            ></div>
            <div class="absolute bottom-6 left-6 text-white">
              <div class="flex items-center gap-4 text-sm mb-2">
                <span
                  class="flex items-center gap-1 bg-white/20 backdrop-blur-sm px-3 py-1 rounded-full"
                >
                  <Icon name="mdi:calendar" class="w-4 h-4" />
                  {{ formatDate(BlogDetails.publish_date) }}
                </span>
                <span
                  class="flex items-center gap-1 bg-white/20 backdrop-blur-sm px-3 py-1 rounded-full"
                >
                  <Icon name="mdi:star" class="w-4 h-4 text-yellow-400" />
                  {{ averageRating }}/5 Rating
                </span>
              </div>
            </div>
          </div>

          <!-- Content -->
          <div class="p-8">
            <h1 class="text-4xl font-bold text-gray-900 mb-6 leading-tight">
              {{ BlogDetails.title }}
            </h1>

            <p class="text-xl text-gray-600 mb-8 leading-relaxed font-medium">
              {{ BlogDetails.short_description }}
            </p>

            <div
              v-html="BlogDetails.description"
              class="prose max-w-none mb-10 text-lg leading-relaxed"
            ></div>

            <!-- Movie Details Box -->
            <div
              class="bg-gradient-to-r from-primary/5 to-secondary/5 rounded-2xl p-6 mb-10 border border-primary/10"
            >
              <h3
                class="text-2xl font-bold text-gray-900 mb-4 flex items-center gap-2"
              >
                <Icon name="mdi:movie" class="text-primary" />
                Movie Details
              </h3>
              <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-sm">
                <div>
                  <p class="font-semibold text-gray-700">Release Date</p>
                  <p class="text-gray-600">January 12, 2024</p>
                </div>
                <div>
                  <p class="font-semibold text-gray-700">Director</p>
                  <p class="text-gray-600">Raj Chakraborty</p>
                </div>
                <div>
                  <p class="font-semibold text-gray-700">Genre</p>
                  <p class="text-gray-600">Action Thriller</p>
                </div>
                <div>
                  <p class="font-semibold text-gray-700">Budget</p>
                  <p class="text-gray-600">5 Crore BDT</p>
                </div>
              </div>
            </div>

            <!-- Reviews Section -->
            <div class="border-t border-gray-200 pt-8">
              <h3
                class="text-3xl font-bold text-gray-900 mb-8 flex items-center gap-3"
              >
                <Icon name="mdi:comment-text-multiple" class="text-primary" />
                Audience Reviews ({{ BlogDetails.blog_reviews.length }})
              </h3>

              <div v-if="BlogDetails.blog_reviews.length > 0" class="space-y-6">
                <div
                  v-for="rev in BlogDetails.blog_reviews"
                  :key="rev.id"
                  class="bg-gray-50 p-6 rounded-2xl border border-gray-200 hover:shadow-lg transition-all duration-300"
                >
                  <div class="flex items-start gap-4 mb-4">
                    <img
                      :src="rev.avatar"
                      :alt="rev.name"
                      class="w-12 h-12 rounded-full object-cover border-2 border-white shadow-md"
                    />
                    <div class="flex-1">
                      <div class="flex items-center justify-between mb-2">
                        <p class="font-semibold text-gray-900 text-lg">
                          {{ rev.name }}
                        </p>
                        <p class="text-sm text-gray-500">
                          {{ formatDate(rev.created_at) }}
                        </p>
                      </div>
                      <div class="flex gap-1 mb-3">
                        <span
                          v-for="star in 5"
                          :key="star"
                          class="text-yellow-500 text-lg"
                        >
                          <span v-if="rev.rating >= star">★</span>
                          <span v-else class="text-gray-300">★</span>
                        </span>
                      </div>
                    </div>
                  </div>
                  <p class="text-gray-700 text-lg leading-relaxed">
                    {{ rev.reviewMassage }}
                  </p>
                </div>
              </div>
              <div v-else class="text-center py-10 text-gray-500">
                <Icon
                  name="mdi:comment-outline"
                  class="w-16 h-16 mx-auto mb-4 text-gray-300"
                />
                <p class="text-xl">No reviews yet. Be the first to review!</p>
              </div>
            </div>

            <!-- Submit Review Form -->
            <div class="border-t border-gray-200 pt-8 mt-12">
              <h3
                class="text-3xl font-bold text-gray-900 mb-8 flex items-center gap-3"
              >
                <Icon name="mdi:pencil" class="text-primary" />
                Share Your Thoughts
              </h3>

              <div
                class="space-y-6 bg-gradient-to-br from-gray-50 to-white p-8 rounded-2xl border border-gray-200"
              >
                <div>
                  <label class="block text-lg font-semibold text-gray-700 mb-3"
                    >Your Rating</label
                  >
                  <div class="flex gap-2">
                    <button
                      v-for="star in 5"
                      :key="star"
                      @click="rating = star"
                      class="text-3xl focus:outline-none transition-transform hover:scale-110 duration-200"
                      :class="
                        rating >= star ? 'text-yellow-500' : 'text-gray-300'
                      "
                    >
                      ★
                    </button>
                  </div>
                </div>

                <div>
                  <label class="block text-lg font-semibold text-gray-700 mb-3"
                    >Your Review</label
                  >
                  <textarea
                    v-model="review.reviewMassage"
                    rows="5"
                    class="w-full p-4 border border-gray-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all text-lg"
                    placeholder="What did you think about Sakib Khan's performance in Tandob?..."
                  ></textarea>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label
                      class="block text-lg font-semibold text-gray-700 mb-3"
                      >Your Name</label
                    >
                    <input
                      v-model="review.name"
                      type="text"
                      class="w-full p-4 border border-gray-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all text-lg"
                      placeholder="Enter your name"
                    />
                  </div>
                  <div>
                    <label
                      class="block text-lg font-semibold text-gray-700 mb-3"
                      >Email Address</label
                    >
                    <input
                      v-model="review.email"
                      type="email"
                      class="w-full p-4 border border-gray-300 rounded-xl focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all text-lg"
                      placeholder="your.email@example.com"
                    />
                  </div>
                </div>

                <button
                  @click="onSubmit"
                  class="w-full bg-gradient-to-r from-primary to-secondary text-white font-bold text-lg px-8 py-4 rounded-xl transition-all duration-300 transform hover:-translate-y-1 shadow-lg hover:shadow-xl"
                >
                  Submit Your Review
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Sidebar - Right Column -->
      <div class="w-full lg:w-1/3 space-y-8">
        <!-- Top Articles -->
        <div class="bg-white rounded-3xl shadow-2xl border border-primary/25 p-6">
          <h3
            class="text-2xl font-bold text-gray-900 mb-6 pb-4 border-b border-gray-200 flex items-center gap-3"
          >
            <Icon name="mdi:fire" class="text-orange-500 text-2xl" />
            Trending News
          </h3>
          <div class="space-y-5">
            <div
              v-for="blog in topArticles"
              :key="blog.id"
              class="flex gap-4 group hover:bg-gray-50 p-4 rounded-xl transition-all duration-300 border border-transparent hover:border-gray-200"
            >
              <img
                :src="blog.blog_image_url"
                class="w-20 h-20 object-cover rounded-xl flex-shrink-0 shadow-md group-hover:shadow-lg transition-all duration-300"
              />
              <div class="flex-1 min-w-0">
                <NuxtLink
                  :to="`/blog-details/${blog.slug}`"
                  class="font-bold text-gray-900 hover:text-primary line-clamp-2 transition-colors text-lg leading-tight"
                >
                  {{ blog.title }}
                </NuxtLink>
                <p class="text-sm text-gray-500 mt-2 flex items-center gap-2">
                  <Icon name="mdi:calendar" class="w-4 h-4" />
                  {{ formatDate(blog.publish_date) }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Latest Articles -->
        <div class="bg-white rounded-3xl shadow-2xl border border-primary/25 p-6">
          <h3
            class="text-2xl font-bold text-gray-900 mb-6 pb-4 border-b border-gray-200 flex items-center gap-3"
          >
            <Icon name="mdi:clock-outline" class="text-blue-500 text-2xl" />
            Latest Updates
          </h3>
          <div class="space-y-5">
            <div
              v-for="blog in latestBlogs"
              :key="blog.id"
              class="flex gap-4 group hover:bg-gray-50 p-4 rounded-xl transition-all duration-300 border border-transparent hover:border-gray-200"
            >
              <img
                :src="blog.blog_image_url"
                class="w-20 h-20 object-cover rounded-xl flex-shrink-0 shadow-md group-hover:shadow-lg transition-all duration-300"
              />
              <div class="flex-1 min-w-0">
                <NuxtLink
                  :to="`/blog-details/${blog.slug}`"
                  class="font-bold text-gray-900 hover:text-primary line-clamp-2 transition-colors text-lg leading-tight"
                >
                  {{ blog.title }}
                </NuxtLink>
                <p class="text-sm text-gray-500 mt-2 flex items-center gap-2">
                  <Icon name="mdi:calendar" class="w-4 h-4" />
                  {{ formatDate(blog.publish_date) }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Newsletter Subscription -->
        <div
          class="bg-gradient-to-r from-primary to-secondary p-6 rounded-3xl shadow-2xl"
        >
          <h3 class="text-xl font-bold text-white mb-3">Stay Updated</h3>
          <p class="text-white/90 text-sm mb-4">
            Get the latest celebrity news and exclusive updates delivered to
            your inbox.
          </p>
          <div class="flex flex-col space-y-3">
            <input
              type="email"
              placeholder="Your email address"
              class="w-full px-4 py-3 rounded-xl bg-white text-sm focus:outline-none focus:ring-2 focus:ring-white"
            />
            <button
              class="w-full px-4 py-3 bg-white text-primary font-bold rounded-xl hover:bg-gray-100 transition-colors text-sm"
            >
              Subscribe Now
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

.prose {
  line-height: 1.8;
  color: #374151;
  font-size: 1.125rem;
}

.prose h3 {
  font-size: 1.5rem;
  font-weight: 700;
  margin-top: 2.5rem;
  margin-bottom: 1.25rem;
  color: #111827;
  border-bottom: 2px solid #e5e7eb;
  padding-bottom: 0.5rem;
}

.prose p {
  margin-bottom: 1.5rem;
}
</style>
