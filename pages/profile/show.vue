<script setup>
const celebrity = {
  id: 1,
  name: "Sakib Khan",
  profession: "Film Actor & Producer",
  category: "Actor",
  image: "/images/sakibKhan.jpg",
  coverImage: "/images/coversakib.png",
  followers: "2.5M",
  following: "245",
  posts: "1.2K",
  rating: 4.8,
  verified: true,
  location: "Dhaka, Bangladesh",
  bio: "Award-winning Bangladeshi film actor known for versatile roles in commercial cinema. One of the highest-paid actors in Bangladesh with numerous box office hits that have redefined the industry standards.",
  stats: {
    movies: 45,
    awards: 12,
    yearsActive: 15,
    upcomingProjects: 3,
  },
  socialMedia: {
    facebook: "sakibkhan.official",
    instagram: "sakibkhan",
    twitter: "sakibkhanbd",
    youtube: "SakibKhanOfficial",
  },
  recentProjects: [
    {
      title: "Tandob",
      year: 2025,
      role: "Lead Actor",
      image: "/images/taandob.jpg",
      rating: 4.8,
      boxOffice: "৳18.3Cr",
    },
    {
      title: "Darad",
      year: 2024,
      role: "Lead Actor",
      image: "/images/dard.jpg",
      rating: 4.4,
      boxOffice: "৳10.2Cr",
    },
    {
      title: "Toofan",
      year: 2024,
      role: "Lead Actor",
      image: "/images/toofan.jpg",
      rating: 4.6,
      boxOffice: "৳15.39Cr",
    },
  ],

  achievements: [
    {
      title: "National Film Award",
      year: 2022,
      description: "Best Actor",
      icon: "heroicons:trophy",
    },
    {
      title: "Meril Prothom Alo Awards",
      year: 2021,
      description: "Popular Actor of the Year",
      icon: "heroicons:star",
    },
    {
      title: "Bachsas Awards",
      year: 2020,
      description: "Best Film Producer",
      icon: "heroicons:film",
    },
    {
      title: "Celebrity of the Year",
      year: 2019,
      description: "Times Bangladesh",
      icon: "heroicons:calendar",
    },
  ],
  gallery: [
    "https://images.unsplash.com/photo-1494790108755-2616b612b786?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1517841905240-472988babdf9?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1529626455594-4ff0802cfb7e?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1492681290082-e932832941e6?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1488426862026-3ee34a7d66df?w=300&h=300&fit=crop",
  ],
  videos: [
    {
      id: "dQw4w9WgXcQ",
      title: "Priyotoma Official Trailer",
      views: "2.4M",
      duration: "2:45",
      thumbnail:
        "https://images.unsplash.com/photo-1489599809505-7c8e1c869b38?w=400&h=225&fit=crop",
      uploadDate: "2023-10-15",
    },
    {
      id: "dQw4w9WgXcQ",
      title: "Behind the Scenes - Nabab",
      views: "1.8M",
      duration: "5:32",
      thumbnail:
        "https://images.unsplash.com/photo-1536440136628-849c177e76a1?w=400&h=225&fit=crop",
      uploadDate: "2022-08-22",
    },
    {
      id: "dQw4w9WgXcQ",
      title: "Interview with Sakib Khan",
      views: "3.1M",
      duration: "8:15",
      thumbnail:
        "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&h=225&fit=crop",
      uploadDate: "2023-05-10",
    },
    {
      id: "dQw4w9WgXcQ",
      title: "Movie Making Documentary",
      views: "1.2M",
      duration: "15:45",
      thumbnail:
        "https://images.unsplash.com/photo-1595769816263-9b910be24d5f?w=400&h=225&fit=crop",
      uploadDate: "2023-02-28",
    },
    {
      id: "dQw4w9WgXcQ",
      title: "Award Acceptance Speech",
      views: "950K",
      duration: "4:20",
      thumbnail:
        "https://images.unsplash.com/photo-1492681290082-e932832941e6?w=400&h=225&fit=crop",
      uploadDate: "2022-12-05",
    },
    {
      id: "dQw4w9WgXcQ",
      title: "Charity Event Highlights",
      views: "1.5M",
      duration: "6:50",
      thumbnail:
        "https://images.unsplash.com/photo-1488426862026-3ee34a7d66df?w=400&h=225&fit=crop",
      uploadDate: "2023-07-18",
    },
  ],
};

const activeTab = ref("overview");
const isFollowing = ref(false);
const showShareModal = ref(false);
const showVideoModal = ref(false);
const selectedVideo = ref(null);

const openVideo = (video) => {
  selectedVideo.value = video;
  showVideoModal.value = true;
};

const formatRelativeDate = (date) => {
  const now = new Date();
  const publishDate = new Date(date);
  const diffTime = Math.abs(now - publishDate);
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));

  if (diffDays === 1) return "1 day ago";
  if (diffDays < 7) return `${diffDays} days ago`;
  if (diffDays < 30) return `${Math.floor(diffDays / 7)} weeks ago`;
  return `${Math.floor(diffDays / 30)} months ago`;
};
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Cover Photo Section -->
    <div class="relative h-80 md:h-[500px] bg-gray-900 overflow-hidden">
      <img
        :src="celebrity.coverImage"
        :alt="`${celebrity.name} cover`"
        class="w-full h-full object-cover object-center"
      />
      <div
        class="absolute inset-0 bg-gradient-to-t from-black/60 via-black/30 to-transparent"
      ></div>

      <!-- Floating Elements -->
      <div
        class="absolute top-20 left-10 w-4 h-4 bg-pink-500/40 rounded-full animate-float"
      ></div>
      <div
        class="absolute top-40 right-20 w-6 h-6 bg-purple-500/30 rounded-full animate-float animation-delay-1000"
      ></div>
      <div
        class="absolute bottom-32 left-24 w-3 h-3 bg-blue-500/40 rounded-full animate-float animation-delay-2000"
      ></div>

      <!-- Back Button -->
      <button
        class="absolute top-6 left-6 p-3 bg-black/50 backdrop-blur-sm rounded-2xl text-white hover:bg-black/70 transition-all duration-300 group"
      >
        <Icon
          name="heroicons:arrow-left"
          class="w-6 h-6 group-hover:-translate-x-1 transition-transform"
        />
      </button>

      <!-- Action Buttons -->
      <div class="absolute top-6 right-6 flex space-x-3">
        <button
          @click="showShareModal = true"
          class="p-3 bg-black/50 backdrop-blur-sm rounded-2xl text-white hover:bg-black/70 transition-all duration-300 group"
        >
          <Icon
            name="heroicons:share"
            class="w-6 h-6 group-hover:scale-110 transition-transform"
          />
        </button>
        <button
          class="p-3 bg-black/50 backdrop-blur-sm rounded-2xl text-white hover:bg-black/70 transition-all duration-300 group"
        >
          <Icon
            name="heroicons:ellipsis-horizontal"
            class="w-6 h-6 group-hover:scale-110 transition-transform"
          />
        </button>
      </div>
    </div>

    <!-- Profile Header -->
    <div class="container mx-auto px-6 -mt-24 relative z-10">
      <div
        class="bg-white/80 backdrop-blur-xl rounded-3xl shadow-2xl border border-white/20"
      >
        <!-- Profile Info -->
        <div class="p-8">
          <div
            class="flex flex-col lg:flex-row items-start lg:items-end space-y-6 lg:space-y-0 lg:space-x-8"
          >
            <!-- Profile Image -->
            <div class="relative">
              <div class="relative group">
                <div
                  class="absolute -inset-4 bg-gradient-to-r from-pink-500 to-purple-600 rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 blur-xl"
                ></div>
                <img
                  :src="celebrity.image"
                  :alt="celebrity.name"
                  class="relative w-32 h-32 lg:w-44 lg:h-44 rounded-2xl object-cover border-4 border-white shadow-2xl z-10"
                />
                <div
                  v-if="celebrity.verified"
                  class="absolute -top-2 -right-2 z-20"
                >
                  <div
                    class="bg-gradient-to-r from-blue-500 to-cyan-500 rounded-full p-2 shadow-lg"
                  >
                    <Icon
                      name="heroicons:check-badge"
                      class="w-5 h-5 text-white"
                    />
                  </div>
                </div>
              </div>
            </div>

            <!-- Profile Details -->
            <div class="flex-1">
              <div
                class="flex flex-col lg:flex-row lg:items-center lg:justify-between"
              >
                <div>
                  <h1
                    class="text-4xl lg:text-6xl font-black text-gray-900 mb-2 bg-gradient-to-r from-gray-900 to-gray-700 bg-clip-text text-transparent"
                  >
                    {{ celebrity.name }}
                  </h1>
                  <p class="text-xl text-gray-600 mb-4 font-medium">
                    {{ celebrity.profession }}
                  </p>

                  <div class="flex flex-wrap items-center gap-4 text-gray-500">
                    <div
                      class="flex items-center space-x-2 bg-gray-100 px-3 py-1.5 rounded-full"
                    >
                      <Icon name="heroicons:map-pin" class="w-4 h-4" />
                      <span class="text-sm font-medium">{{
                        celebrity.location
                      }}</span>
                    </div>
                    <div
                      class="flex items-center space-x-2 bg-yellow-100 px-3 py-1.5 rounded-full"
                    >
                      <Icon
                        name="heroicons:star"
                        class="w-4 h-4 text-yellow-600"
                      />
                      <span class="text-sm font-semibold text-yellow-700">{{
                        celebrity.rating
                      }}</span>
                    </div>
                    <div
                      class="flex items-center space-x-2 bg-blue-100 px-3 py-1.5 rounded-full"
                    >
                      <Icon
                        name="heroicons:calendar"
                        class="w-4 h-4 text-blue-600"
                      />
                      <span class="text-sm font-medium text-blue-700"
                        >{{ celebrity.stats.yearsActive }} years</span
                      >
                    </div>
                  </div>
                </div>

                <!-- Action Buttons -->
                <div class="flex space-x-4 mt-6 lg:mt-0">
                  <button
                    @click="isFollowing = !isFollowing"
                    :class="[
                      'px-8 py-3 rounded-2xl font-semibold transition-all duration-300 transform hover:-translate-y-1 hover:shadow-lg',
                      isFollowing
                        ? 'bg-gray-100 text-gray-700 border border-gray-300 hover:bg-gray-200'
                        : 'bg-gradient-to-r from-primary to-secondary text-white hover:from-pink-600 hover:to-purple-700',
                    ]"
                  >
                    <span class="flex items-center space-x-2">
                      <Icon
                        :name="
                          isFollowing ? 'heroicons:check' : 'heroicons:plus'
                        "
                        class="w-4 h-4"
                      />
                      <span>{{ isFollowing ? "Following" : "Follow" }}</span>
                    </span>
                  </button>
                  <button
                    class="px-6 py-3 border-2 border-primary text-primary rounded-2xl font-semibold hover:border-gray-400 hover:bg-gray-50 transition-all duration-300 transform hover:-translate-y-1"
                  >
                    <Icon name="heroicons:envelope" class="w-5 h-5" />
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Bio -->
          <div class="mt-8 max-w-4xl">
            <p
              class="text-gray-600 text-lg leading-relaxed bg-gradient-to-r from-gray-600 to-gray-800 bg-clip-text text-transparent font-medium"
            >
              {{ celebrity.bio }}
            </p>
          </div>

          <!-- Stats -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mt-8">
            <div
              v-for="(stat, key, index) in celebrity.stats"
              :key="key"
              class="group text-center p-6 bg-gradient-to-br from-primary/15 to-secondary/15 rounded-2xl border border-primary/15 hover:border-pink-200 transition-all duration-500 hover:-translate-y-2 hover:shadow-xl cursor-pointer"
            >
              <div
                class="text-3xl font-black bg-gradient-to-r from-primary to-secondary bg-clip-text text-transparent"
              >
                {{ stat }}+
              </div>
              <div class="text-gray-900 mt-2 font-medium capitalize">
                {{ key.replace(/([A-Z])/g, " $1").trim() }}
              </div>
            </div>
          </div>
        </div>

        <!-- Navigation Tabs -->
        <div class="border-t border-gray-200/50">
          <div class="flex overflow-x-auto px-8 gap-5">
            <button
              v-for="tab in [
                'overview',
                'projects',
                'gallery',
                'videos',
                'achievements',
              ]"
              :key="tab"
              @click="activeTab = tab"
              :class="[
                'px-6 py-3 rounded-lg font-semibold transition-all duration-300 transform',
                activeTab === tab
                  ? 'bg-gradient-to-r from-primary to-secondary text-white shadow-lg'
                  : 'bg-gray-200 text-gray-700 border border-gray-200 hover:border-primary/30 hover:shadow-md',
              ]"
            >
              <span class="flex items-center space-x-2">
                <Icon
                  :name="getTabIcon(tab)"
                  class="w-5 h-5 transition-transform group-hover:scale-110"
                />
                <span>{{ tab.charAt(0).toUpperCase() + tab.slice(1) }}</span>
              </span>
            </button>
          </div>
        </div>

        <!-- Tab Content -->
        <div class="p-8">
          <!-- Overview Tab -->
          <div v-if="activeTab === 'overview'" class="space-y-12">
            <!-- Recent Projects -->
            <div>
              <h3 class="text-3xl font-bold text-gray-900 mb-8">
                Recent Projects
              </h3>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div
                  v-for="project in celebrity.recentProjects"
                  :key="project.title"
                  class="group bg-white rounded-3xl shadow-lg border border-gray-200 overflow-hidden hover:shadow-2xl transition-all duration-500 hover:-translate-y-3"
                >
                  <div class="relative h-60 overflow-hidden">
                    <img
                      :src="project.image"
                      :alt="project.title"
                      class="w-full h-full object-cover object-top transition-transform duration-700 group-hover:scale-110"
                    />
                    <div
                      class="absolute top-4 right-4 bg-black/80 text-white px-3 py-1 rounded-full text-sm font-semibold backdrop-blur-sm"
                    >
                      {{ project.year }}
                    </div>
                    <div
                      class="absolute bottom-4 left-4 bg-gradient-to-r from-pink-500 to-purple-600 text-white px-3 py-1 rounded-full text-sm font-semibold"
                    >
                      {{ project.boxOffice }}
                    </div>
                  </div>
                  <div class="p-6">
                    <h4 class="text-xl font-bold text-gray-900 mb-2">
                      {{ project.title }}
                    </h4>
                    <p class="text-gray-600 mb-3 font-medium">
                      {{ project.role }}
                    </p>
                    <div class="flex items-center justify-between">
                      <div class="flex items-center space-x-1">
                        <Icon
                          name="heroicons:star"
                          class="w-4 h-4 text-yellow-500"
                        />
                        <span class="text-gray-700 font-semibold">{{
                          project.rating
                        }}</span>
                      </div>
                      <button
                        class="text-pink-600 font-semibold hover:text-pink-700 transition-colors flex items-center space-x-1"
                      >
                        <span>Details</span>
                        <Icon name="heroicons:arrow-right" class="w-4 h-4" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Social Media -->
            <div>
              <h3 class="text-3xl font-bold text-gray-900 mb-6">
                Connect With Me
              </h3>
              <div class="flex flex-wrap gap-4">
                <a
                  v-for="(username, platform) in celebrity.socialMedia"
                  :key="platform"
                  :href="`https://${platform}.com/${username}`"
                  target="_blank"
                  class="group flex items-center space-x-3 px-6 py-4 bg-white rounded-2xl shadow-lg border border-primary/15 hover:shadow-xl transition-all duration-300 transform hover:-translate-y-2"
                >
                  <div
                    class="p-2 rounded-xl bg-gradient-to-r from-primary to-secondary group-hover:scale-110 transition-transform duration-300"
                  >
                    <Icon
                      :name="`mdi:${platform}`"
                      class="w-4 h-4 text-white"
                    />
                  </div>
                  <div>
                    <div class="font-semibold text-gray-900">
                      @{{ username }}
                    </div>
                    <div class="text-sm text-gray-500 capitalize">
                      {{ platform }}
                    </div>
                  </div>
                </a>
              </div>
            </div>
          </div>

          <!-- Videos Tab -->
          <div v-if="activeTab === 'videos'" class="space-y-8">
            <div class="flex items-center justify-between">
              <h3 class="text-3xl font-bold text-gray-900">Video Gallery</h3>
              <div class="text-gray-500">
                {{ celebrity.videos.length }} videos
              </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
              <div
                v-for="video in celebrity.videos"
                :key="video.id"
                @click="openVideo(video)"
                class="group bg-white rounded-2xl shadow-lg border border-gray-200 overflow-hidden hover:shadow-xl transition-all duration-500 hover:-translate-y-2 cursor-pointer"
              >
                <div class="relative aspect-video overflow-hidden">
                  <img
                    :src="video.thumbnail"
                    :alt="video.title"
                    class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
                  />
                  <div
                    class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                  ></div>

                  <!-- Play Button -->
                  <div
                    class="absolute inset-0 flex items-center justify-center"
                  >
                    <div
                      class="w-16 h-16 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center transform scale-90 group-hover:scale-100 transition-transform duration-300"
                    >
                      <Icon
                        name="heroicons:play"
                        class="w-8 h-8 text-white ml-1"
                      />
                    </div>
                  </div>

                  <!-- Duration -->
                  <div
                    class="absolute bottom-3 right-3 bg-black/80 text-white px-2 py-1 rounded text-sm font-medium"
                  >
                    {{ video.duration }}
                  </div>
                </div>

                <div class="p-4">
                  <h4 class="font-semibold text-gray-900 mb-2 line-clamp-2">
                    {{ video.title }}
                  </h4>
                  <div
                    class="flex items-center justify-between text-sm text-gray-500"
                  >
                    <span>{{ video.views }} views</span>
                    <span>{{ formatRelativeDate(video.uploadDate) }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Other tabs remain similar but updated with modern design -->
          <!-- Gallery Tab -->
          <div v-if="activeTab === 'gallery'" class="space-y-8">
            <h3 class="text-3xl font-bold text-gray-900">Photo Gallery</h3>
            <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
              <div
                v-for="(image, index) in celebrity.gallery"
                :key="index"
                class="group aspect-square rounded-2xl overflow-hidden shadow-lg hover:shadow-xl transition-all duration-500 hover:-translate-y-2 cursor-pointer"
              >
                <img
                  :src="image"
                  :alt="`${celebrity.name} gallery image ${index + 1}`"
                  class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
                />
              </div>
            </div>
          </div>

          <!-- Achievements Tab -->
          <div v-if="activeTab === 'achievements'" class="space-y-6">
            <h3 class="text-3xl font-bold text-gray-900">
              Awards & Achievements
            </h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div
                v-for="achievement in celebrity.achievements"
                :key="achievement.title"
                class="group bg-white rounded-2xl shadow-lg border border-gray-200 p-6 hover:shadow-xl transition-all duration-500 hover:-translate-y-2"
              >
                <div class="flex items-center space-x-4">
                  <div
                    class="p-3 bg-gradient-to-r from-pink-500 to-purple-600 rounded-xl"
                  >
                    <Icon :name="achievement.icon" class="w-6 h-6 text-white" />
                  </div>
                  <div class="flex-1">
                    <h4 class="text-xl font-bold text-gray-900 mb-1">
                      {{ achievement.title }}
                    </h4>
                    <p class="text-gray-600">{{ achievement.description }}</p>
                  </div>
                  <div class="text-right">
                    <div class="text-2xl font-black text-pink-500">
                      {{ achievement.year }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Video Modal -->
  <UModal v-model="showVideoModal" size="4xl" :title="selectedVideo?.title">
    <template #body>
      <div class="aspect-video w-full bg-black rounded-lg overflow-hidden">
        <iframe
          v-if="showVideoModal && selectedVideo"
          class="w-full h-full"
          :src="`https://www.youtube.com/embed/${selectedVideo.id}?autoplay=1`"
          :title="selectedVideo.title"
          frameborder="0"
          allow="autoplay; encrypted-media"
          allowfullscreen
        ></iframe>
      </div>
      <div v-if="selectedVideo" class="p-6">
        <h3 class="text-xl font-bold text-gray-900 mb-2">
          {{ selectedVideo.title }}
        </h3>
        <div class="flex items-center space-x-4 text-gray-500 text-sm">
          <span>{{ selectedVideo.views }} views</span>
          <span>•</span>
          <span>{{ formatRelativeDate(selectedVideo.uploadDate) }}</span>
        </div>
      </div>
    </template>
  </UModal>

  <!-- Share Modal -->
  <UModal v-model="showShareModal" title="Share Profile">
    <template #body>
      <div class="p-6">
        <div class="flex justify-center space-x-6 mb-8">
          <button
            v-for="platform in ['facebook', 'instagram', 'twitter', 'whatsapp']"
            :key="platform"
            :class="`p-4 rounded-2xl text-white hover:scale-110 transition-transform duration-300 ${getPlatformColor(
              platform
            )}`"
          >
            <Icon :name="`mdi:${platform}`" class="w-8 h-8" />
          </button>
        </div>
        <div class="flex space-x-3">
          <input
            type="text"
            :value="`https://celebbd.com/${celebrity.name
              .toLowerCase()
              .replace(' ', '-')}`"
            class="flex-1 px-4 py-3 border border-gray-300 rounded-2xl focus:outline-none focus:ring-2 focus:ring-pink-500"
            readonly
          />
          <button
            class="px-6 py-3 bg-gradient-to-r from-pink-500 to-purple-600 text-white rounded-2xl font-semibold hover:from-pink-600 hover:to-purple-700 transition-all duration-300"
          >
            Copy Link
          </button>
        </div>
      </div>
    </template>
  </UModal>
</template>

<script>
// Helper functions
export default {
  methods: {
    getTabIcon(tab) {
      const icons = {
        overview: "heroicons:home",
        projects: "heroicons:film",
        gallery: "heroicons:photo",
        videos: "heroicons:play",
        achievements: "heroicons:trophy",
      };
      return icons[tab] || "heroicons:document";
    },
    getPlatformColor(platform) {
      const colors = {
        facebook: "bg-blue-500 hover:bg-blue-600",
        instagram: "bg-pink-500 hover:bg-pink-600",
        twitter: "bg-blue-400 hover:bg-blue-500",
        whatsapp: "bg-green-500 hover:bg-green-600",
      };
      return colors[platform] || "bg-gray-500";
    },
  },
};
</script>

<style scoped>
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

/* Hide scrollbar for tabs */
.tabs-container::-webkit-scrollbar {
  display: none;
}

.tabs-container {
  scrollbar-width: none;
}
</style>
