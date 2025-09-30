<script setup>
const activeMenu = ref(null);
const searchQuery = ref("");
const isMobileMenuOpen = ref(false);

const menus = [
  {
    title: "Home",
    items: [
      { title: "Featured Celebrities", icon: "mdi:star" },
      { title: "Latest News", icon: "mdi:newspaper-variant" },
      { title: "Exclusive Content", icon: "mdi:crown" },
      { title: "VIP Access", icon: "mdi:lock-open" },
    ],
  },
  {
    title: "Categories",
    items: [
      { title: "Movie Stars", icon: "mdi:movie" },
      { title: "Musicians", icon: "mdi:music" },
      { title: "YouTubers", icon: "mdi:youtube" },
      { title: "Sports Stars", icon: "mdi:trophy" },
      { title: "Influencers", icon: "mdi:instagram" },
      { title: "Bloggers", icon: "mdi:pen" },
    ],
  },
  {
    title: "Top Stars",
    items: [
      { title: "Trending Now", icon: "mdi:trending-up" },
      { title: "Most Followed", icon: "mdi:account-group" },
      { title: "Highest Paid", icon: "mdi:currency-usd" },
      { title: "Award Winners", icon: "mdi:award" },
    ],
  },
  {
    title: "Future Stars",
    items: [
      { title: "Rising Talents", icon: "mdi:rocket" },
      { title: "Breakout Artists", icon: "mdi:chart-line" },
      { title: "Underrated Gems", icon: "mdi:diamond" },
      { title: "Ones to Watch", icon: "mdi:eye" },
    ],
  },
  {
    title: "Blog",
    items: [
      { title: "Celebrity Interviews", icon: "mdi:microphone" },
      { title: "Behind the Scenes", icon: "mdi:video" },
      { title: "Style & Fashion", icon: "mdi:hanger" },
      { title: "Lifestyle", icon: "mdi:palette" },
    ],
  },
];

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
};

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false;
};
</script>

<template>
  <header
    class="sticky top-0 z-50 primary/15 backdrop-blur-md border-b border-[#6b1fad]/50 shadow-xl"
  >
    <div class="container mx-auto px-4">
      <div class="flex items-center justify-between h-24">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center group relative" @click="closeMobileMenu">
          <img
            src="/images/Logo6.png"
            alt="Celebrity Hub"
            class="h-auto w-28 rounded-full"
          />
        </NuxtLink>

        <!-- Desktop Menu -->
        <nav class="hidden lg:flex items-center space-x-1">
          <div
            v-for="(menu, index) in menus"
            :key="index"
            @mouseenter="activeMenu = index"
            @mouseleave="activeMenu = null"
            class="relative"
          >
            <button
              class="px-4 py-2 text-black font-medium hover:text-primary transition-all flex items-center group relative"
              :class="{ 'text-primary': activeMenu === index }"
            >
              <span class="relative z-10">{{ menu.title }}</span>
              <span
                class="absolute bottom-0 left-1/2 w-0 h-0.5 bg-primary transform -translate-x-1/2 transition-all duration-300 group-hover:w-4/5"
                :class="{ 'w-4/5': activeMenu === index }"
              ></span>
              <Icon
                name="mdi:chevron-down"
                class="ml-1.5 text-primary text-lg transition-transform duration-200 group-hover:rotate-180 group-hover:text-primary"
                :class="{ 'rotate-180 text-primary': activeMenu === index }"
              />
            </button>

            <!-- Modern Dropdown Menu -->
            <transition name="dropdown">
              <div
                v-if="activeMenu === index"
                class="absolute left-1/2 transform -translate-x-1/2 mt-3 w-72 bg-white backdrop-blur-lg rounded-xl shadow-2xl z-50 overflow-hidden border border-secondary/25"
              >
                <div class="py-2">
                  <NuxtLink
                    v-for="(item, i) in menu.items"
                    :key="i"
                    to="#"
                    class="px-5 py-3 flex items-center text-black hover:text-primary transition-all duration-200 group border-b border-gray-700/50 last:border-b-0"
                  >
                    <Icon
                      :name="item.icon"
                      class="mr-3 text-primary text-lg group-hover:scale-110 transition-transform"
                    />
                    <span class="font-medium">{{ item.title }}</span>
                    <Icon
                      name="mdi:chevron-right"
                      class="ml-auto text-primary group-hover:text-[#ff3131] transition-colors"
                    />
                  </NuxtLink>
                </div>
              </div>
            </transition>
          </div>
        </nav>

        <!-- Search + CTA -->
        <div class="flex items-center space-x-4">
          <!-- Search Bar -->
          <div class="relative hidden md:block">
            <div class="relative group">
              <input
                v-model="searchQuery"
                type="text"
                placeholder="Search celebrities, movies, news..."
                class="pl-12 pr-5 py-3 border border-primary/25 bg-white rounded-full focus:ring-primary/50 focus:bg-primary/25 w-56 transition-all duration-300 group-hover:w-64 focus:w-64 shadow-inner text-white placeholder-gray-500"
              />
              <div
                class="absolute inset-y-0 left-0 flex items-center pl-4 pointer-events-none"
              >
                <Icon
                  name="mdi:magnify"
                  class="text-xl text-primary group-hover:text-[#ff3131] transition-colors"
                />
              </div>
              <button
                v-if="searchQuery"
                @click="searchQuery = ''"
                class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-400 hover:text-[#ff3131] transition-colors"
              >
                <Icon name="mdi:close" class="text-lg" />
              </button>
            </div>
          </div>

          <!-- CTA Button -->
          <NuxtLink
            to="#"
            class="hidden  border-2 border-white xl:flex items-center px-6 py-2.5 bg-gradient-to-r from-primary to-secondary text-white font-medium rounded-full shadow-lg hover:shadow-xl transition-all hover:scale-[1.02] group"
          >
            <Icon
              name="material-symbols:account-circle"
              class="mr-2 text-lg group-hover:scale-110 transition-transform"
            />
            <span>Submit Profile</span>
          </NuxtLink>

          <!-- Mobile Menu Toggle -->
          <button
            @click="toggleMobileMenu"
            class="lg:hidden p-2.5 rounded-full bg-gray-800/80 hover:bg-gray-700 transition-colors"
          >
            <Icon 
              :name="isMobileMenuOpen ? 'mdi:close' : 'mdi:menu'" 
              class="text-2xl text-white" 
            />
          </button>
        </div>
      </div>

      <!-- Mobile Menu -->
      <transition name="mobile-menu">
        <div
          v-if="isMobileMenuOpen"
          class="lg:hidden bg-gray-800/95 backdrop-blur-lg rounded-xl mt-2 shadow-2xl border border-[#6b1fad]/50 overflow-hidden"
        >
          <div class="py-4">
            <div
              v-for="(menu, index) in menus"
              :key="index"
              class="border-b border-gray-700/50 last:border-b-0"
            >
              <button
                @click="activeMenu = activeMenu === index ? null : index"
                class="w-full px-5 py-3 flex items-center justify-between text-gray-200 hover:bg-[#6b1fad]/30 transition-all"
              >
                <span class="font-medium">{{ menu.title }}</span>
                <Icon
                  name="mdi:chevron-down"
                  class="text-lg transition-transform duration-200"
                  :class="{ 'rotate-180': activeMenu === index }"
                />
              </button>
              
              <div
                v-if="activeMenu === index"
                class="bg-gray-900/50 pl-5"
              >
                <NuxtLink
                  v-for="(item, i) in menu.items"
                  :key="i"
                  to="#"
                  @click="closeMobileMenu"
                  class="block px-5 py-3 flex items-center text-gray-300 hover:text-white transition-colors border-b border-gray-800 last:border-b-0"
                >
                  <Icon
                    :name="item.icon"
                    class="mr-3 text-[#ff3131] text-lg"
                  />
                  <span>{{ item.title }}</span>
                </NuxtLink>
              </div>
            </div>
            
            <!-- Mobile Search -->
            <div class="px-5 py-4 border-t border-gray-700/50">
              <div class="relative">
                <input
                  v-model="searchQuery"
                  type="text"
                  placeholder="Search celebrities..."
                  class="w-full pl-12 pr-5 py-3 border-0 bg-gray-700 rounded-full focus:ring-2 focus:ring-[#ff3131]/50 text-white placeholder-gray-400"
                />
                <div
                  class="absolute inset-y-0 left-0 flex items-center pl-4 pointer-events-none"
                >
                  <Icon
                    name="mdi:magnify"
                    class="text-xl text-gray-400"
                  />
                </div>
              </div>
            </div>
            
            <!-- Mobile Submit Profile Button -->
            <div class="px-5 pb-4">
              <NuxtLink
                to="#"
                @click="closeMobileMenu"
                class="block w-full text-center px-6 py-3 bg-gradient-to-r from-[#6b1fad] to-[#ff3131] text-white font-medium rounded-full shadow-lg transition-all"
              >
                Submit Profile
              </NuxtLink>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </header>
</template>

<style scoped>
.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}
.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px) translateX(-50%);
}

.mobile-menu-enter-active,
.mobile-menu-leave-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.mobile-menu-enter-from,
.mobile-menu-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>