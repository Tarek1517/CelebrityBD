<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100"
  >
    <!-- Cover Photo Section -->
    <div class="relative h-80 md:h-[400px] bg-gray-900 overflow-hidden">
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
    </div>

    <!-- Profile Header -->
    <div class="container mx-auto px-6 -mt-24 relative z-10">
      <div class="bg-white/80 rounded-3xl">
        <!-- Profile Info -->
        <div
          class="p-8 backdrop-blur-xl rounded-3xl shadow-2xl border border-primary border-white/20"
        >
          <div
            class="flex flex-col lg:flex-row items-start lg:items-end space-y-6 lg:space-y-0 lg:space-x-8"
          >
            <!-- Profile Image -->
            <div class="relative">
              <div class="relative group">
                <div
                  class="absolute -inset-4 bg-gradient-to-r from-primary/15 to-primary/15 rounded-3xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 blur-xl"
                ></div>
                <img
                  :src="celebrity.image"
                  :alt="celebrity.name"
                  class="relative w-32 h-32 lg:w-44 lg:h-44 rounded-2xl object-cover border-4 border-white shadow-2xl z-10"
                />
                <button
                  @click="showImageUpload = true"
                  class="absolute bottom-2 right-2 bg-black/80 text-white p-2 rounded-full hover:bg-black transition-all duration-300 transform hover:scale-110"
                >
                  <Icon name="heroicons:camera" class="w-4 h-4" />
                </button>

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
                      class="flex items-center space-x-2 bg-primary/15 text-primary px-3 py-1.5 rounded-full"
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

                <!-- Update & Logout Buttons -->
                <div
                  class="flex flex-col lg:flex-row items-stretch gap-3 mt-6 lg:mt-0"
                >
                  <button
                    @click="handleLogout"
                    class="px-6 py-3 rounded-xl font-semibold bg-rose-500 text-white hover:bg-rose-600 hover:shadow-lg transition-all duration-300 flex items-center justify-center space-x-2"
                  >
                    <Icon
                      name="heroicons:arrow-left-on-rectangle"
                      class="w-5 h-5"
                    />
                    <span>Logout</span>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="flex min-h-screen bg-gray-50 mt-12">
          <!-- Sidebar Navigation -->
          <div class="w-80 bg-white border-r border-gray-200 p-6">
            <div class="space-y-2">
              <button
                v-for="tab in [
                  'overview',
                  'edit-profile',
                  'projects',
                  'gallery',
                  'videos',
                  'achievements',
                ]"
                :key="tab"
                @click="activeTab = tab"
                :class="[
                  'w-full px-6 py-4 rounded-xl font-semibold transition-all duration-300 transform text-left',
                  activeTab === tab
                    ? 'bg-gradient-to-r from-primary to-secondary text-white shadow-lg'
                    : 'bg-gray-100 text-gray-700 border border-gray-200 hover:border-primary/30 hover:shadow-md',
                ]"
              >
                <span class="flex items-center space-x-3">
                  <Icon
                    :name="getTabIcon(tab)"
                    class="w-5 h-5 transition-transform group-hover:scale-110"
                  />
                  <span>{{ tab.charAt(0).toUpperCase() + tab.slice(1) }}</span>
                </span>
              </button>
            </div>
          </div>

          <!-- Main Content -->
          <div class="flex-1 p-8">
            <!-- Tab Content -->
            <div class="max-w-6xl mx-auto">
              <!-- Navigation Tabs -->

              <div v-if="activeTab === 'overview'" class="space-y-12">
                <!-- Recent Projects -->
                <div>
                  <div class="flex justify-between items-center mb-8">
                    <h3 class="text-3xl font-bold text-gray-900">
                      Recent Projects
                    </h3>
                  </div>
                  <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <div
                      v-for="project in celebrity.recentProjects"
                      :key="project.title"
                      class="group bg-white rounded-3xl shadow-lg border border-primary/20 overflow-hidden hover:shadow-2xl transition-all duration-500 hover:-translate-y-3"
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
                            <Icon
                              name="heroicons:arrow-right"
                              class="w-4 h-4"
                            />
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Social Media -->
                <div>
                  <div class="flex justify-between items-center mb-6">
                    <h3 class="text-3xl font-bold text-gray-900">
                      Connect With Me
                    </h3>
                    <button
                      @click="openModal('social')"
                      class="flex items-center space-x-2 px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
                    >
                      <Icon name="heroicons:plus" class="w-4 h-4" />
                      <span>Add Social</span>
                    </button>
                  </div>
                  <div class="flex flex-wrap gap-4">
                    <a
                      v-for="(username, platform) in celebrity.socialMedia"
                      :key="platform"
                      :href="`https://${platform}.com/${username}`"
                      target="_blank"
                      class="group flex items-center space-x-3 px-6 py-4 bg-white rounded-2xl shadow-lg border border-primary/25 hover:shadow-xl transition-all duration-300 transform hover:-translate-y-2"
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

              <!-- Projects Tab -->
              <div v-if="activeTab === 'projects'" class="space-y-8">
                <div class="flex justify-between items-center">
                  <h3 class="text-3xl font-bold text-gray-900">All Projects</h3>
                </div>

                <!-- Add Project Form -->
                <div
                  class="bg-white rounded-2xl shadow-lg border border-gray-200 p-6"
                >
                  <h4 class="text-xl font-bold text-gray-900 mb-6">
                    Add New Project
                  </h4>
                  <form @submit.prevent="addProject" class="space-y-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Project Title</label
                        >
                        <input
                          v-model="newProject.title"
                          type="text"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Year</label
                        >
                        <input
                          v-model="newProject.year"
                          type="number"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Role</label
                        >
                        <input
                          v-model="newProject.role"
                          type="text"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Box Office Collection</label
                        >
                        <input
                          v-model="newProject.boxOffice"
                          type="text"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Rating</label
                        >
                        <input
                          v-model="newProject.rating"
                          type="number"
                          step="0.1"
                          min="0"
                          max="5"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                      <div>
                        <label
                          class="block text-sm font-medium text-gray-700 mb-2"
                          >Image URL</label
                        >
                        <input
                          v-model="newProject.image"
                          type="url"
                          class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
                          required
                        />
                      </div>
                    </div>
                    <!-- Cover Image - 2/3 width -->
                    <div class="space-y-2 lg:col-span-2">
                      <label
                        class="flex items-center text-sm font-medium text-gray-700"
                      >
                        <Icon
                          name="mdi:image-outline"
                          class="w-4 h-4 mr-2 text-primary"
                        />
                        Cover Image <span class="text-red-500 ml-1">*</span>
                      </label>
                      <label
                        for="cover_image"
                        class="block w-full h-64 flex items-center justify-center gap-3 p-4 border-2 border-dashed border-primary/30 rounded-xl text-primary cursor-pointer bg-gradient-to-br from-primary/5 to-secondary/5 hover:from-primary/10 hover:to-secondary/10 transition-all duration-300 group"
                      >
                        <input
                          type="file"
                          id="cover_image"
                          hidden
                          @change="onCoverFileChange"
                        />
                        <div v-if="!coverImg" class="text-center">
                          <Icon
                            name="mdi:cloud-upload-outline"
                            class="w-8 h-8 mx-auto mb-2 text-primary group-hover:scale-110 transition-transform duration-300"
                          />
                          <p class="text-sm font-medium text-gray-700">
                            Upload Cover Photo
                          </p>
                          <p class="text-xs text-gray-500 mt-1">
                            PNG, JPG, WEBP up to 5MB
                          </p>
                        </div>
                        <div v-else class="relative w-full h-full">
                          <img
                            :src="coverImg"
                            class="w-full h-full object-cover rounded-lg shadow-md"
                          />
                          <div
                            class="absolute inset-0 bg-black/40 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-lg flex items-center justify-center"
                          >
                            <Icon
                              name="mdi:camera-plus"
                              class="w-8 h-8 text-white"
                            />
                          </div>
                        </div>
                      </label>
                    </div>
                    <div class="flex justify-end space-x-4">
                      <button
                        @click="showProjectForm = false"
                        type="button"
                        class="px-6 py-3 border border-primary/25 text-primary rounded-lg hover:bg-gray-50 transition-colors"
                      >
                        Cancel
                      </button>
                      <button
                        type="submit"
                        class="px-6 py-3 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
                      >
                        Add Project
                      </button>
                    </div>
                  </form>
                </div>
              </div>

              <!-- Gallery Tab -->
              <div v-if="activeTab === 'gallery'" class="space-y-8">
                <div class="flex justify-between items-center">
                  <h3 class="text-3xl font-bold text-gray-900">
                    Photo Gallery
                  </h3>
                  <button
                    @click="openModal('gallery')"
                    class="flex items-center space-x-2 px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
                  >
                    <Icon name="heroicons:plus" class="w-4 h-4" />
                    <span>Add Photos</span>
                  </button>
                </div>
                <div
                  class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4"
                >
                  <div
                    v-for="(image, index) in celebrity.gallery"
                    :key="index"
                    @click="
                      openImageModal(
                        image,
                        `${celebrity.name} - Gallery Image ${index + 1}`
                      )
                    "
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

              <div v-if="activeTab === 'videos'" class="space-y-8">
                <div class="flex justify-between items-center">
                  <h3 class="text-3xl font-bold text-gray-900">
                    Video Gallery
                  </h3>
                  <button
                    @click="openModal('video')"
                    class="flex items-center space-x-2 px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
                  >
                    <Icon name="heroicons:plus" class="w-4 h-4" />
                    <span>Add Video</span>
                  </button>
                </div>
                <div
                  class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"
                >
                  <div
                    v-for="video in celebrity.videos"
                    :key="video.id"
                    @click="openVideoModal(video)"
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

              <!-- Achievements Tab -->
              <div v-if="activeTab === 'achievements'" class="space-y-6">
                <div class="flex justify-between items-center">
                  <h3 class="text-3xl font-bold text-gray-900">
                    Awards & Achievements
                  </h3>
                  <button
                    @click="openModal('achievement')"
                    class="flex items-center space-x-2 px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
                  >
                    <Icon name="heroicons:plus" class="w-4 h-4" />
                    <span>Add Achievement</span>
                  </button>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div
                    v-for="achievement in celebrity.achievements"
                    :key="achievement.title"
                    class="group bg-white rounded-2xl shadow-lg border border-primary/35 p-6 hover:shadow-xl transition-all duration-500 hover:-translate-y-2"
                  >
                    <div class="flex items-center space-x-4">
                      <div
                        class="p-3 bg-gradient-to-r from-pink-500 to-purple-600 rounded-xl"
                      >
                        <Icon
                          :name="achievement.icon"
                          class="w-6 h-6 text-white"
                        />
                      </div>
                      <div class="flex-1">
                        <h4 class="text-xl font-bold text-gray-900 mb-1">
                          {{ achievement.title }}
                        </h4>
                        <p class="text-gray-600">
                          {{ achievement.description }}
                        </p>
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

              <!-- Edit Profile Tab -->
              <div v-if="activeTab === 'edit-profile'" class="space-y-8">
                <h3 class="text-3xl font-bold text-gray-900">Edit Profile</h3>

                <!-- Basic Information -->
                <div
                  class="bg-white rounded-2xl shadow-lg border border-gray-200 p-6"
                >
                  <h4 class="text-xl font-bold text-gray-900 mb-6">
                    Basic Information
                  </h4>
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div>
                      <label
                        class="block text-sm font-medium text-gray-700 mb-2"
                        >Full Name</label
                      >
                      <input
                        v-model="celebrity.name"
                        type="text"
                        class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                      />
                    </div>
                    <div>
                      <label
                        class="block text-sm font-medium text-gray-700 mb-2"
                        >Profession</label
                      >
                      <input
                        v-model="celebrity.profession"
                        type="text"
                        class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                      />
                    </div>
                    <div>
                      <label
                        class="block text-sm font-medium text-gray-700 mb-2"
                        >Location</label
                      >
                      <input
                        v-model="celebrity.location"
                        type="text"
                        class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                      />
                    </div>
                    <div>
                      <label
                        class="block text-sm font-medium text-gray-700 mb-2"
                        >Rating</label
                      >
                      <input
                        v-model="celebrity.rating"
                        type="number"
                        step="0.1"
                        min="0"
                        max="5"
                        class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                      />
                    </div>
                  </div>
                </div>

                <!-- Bio Section -->
                <div
                  class="bg-white rounded-2xl shadow-lg border border-gray-200 p-6"
                >
                  <h4 class="text-xl font-bold text-gray-900 mb-6">Bio</h4>
                  <textarea
                    v-model="celebrity.bio"
                    rows="4"
                    class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                  ></textarea>
                </div>

                <!-- Stats Section -->
                <div
                  class="bg-white rounded-2xl shadow-lg border border-gray-200 p-6"
                >
                  <h4 class="text-xl font-bold text-gray-900 mb-6">
                    Career Stats
                  </h4>
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div v-for="(stat, key) in celebrity.stats" :key="key">
                      <label
                        class="block text-sm font-medium text-gray-700 mb-2 capitalize"
                        >{{ key.replace(/([A-Z])/g, " $1").trim() }}</label
                      >
                      <input
                        v-model="celebrity.stats[key]"
                        type="number"
                        class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition placeholder-gray-400"
                      />
                    </div>
                  </div>
                </div>

                <!-- Save Button -->
                <div class="flex justify-end">
                  <button
                    @click="saveProfile"
                    class="px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white rounded-2xl font-semibold transition-all duration-300 transform hover:-translate-y-1 hover:shadow-lg"
                  >
                    Save Changes
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modals -->
    <Modal
      :isOpen="isModalOpened"
      @modal-close="closeModal"
      :title="modalTitle"
    >
      <!-- Social Media Modal -->
      <div v-if="modalType === 'social'" class="p-6">
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Platform</label
            >
            <select
              v-model="newSocial.platform"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            >
              <option value="facebook">Facebook</option>
              <option value="instagram">Instagram</option>
              <option value="twitter">Twitter</option>
              <option value="youtube">YouTube</option>
            </select>
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Username</label
            >
            <input
              v-model="newSocial.username"
              type="text"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
              placeholder="@username"
            />
          </div>
        </div>
        <div class="flex justify-end space-x-4 mt-6">
          <button
            @click="closeModal"
            class="px-6 py-3 border border-primary/25 text-primary rounded-lg hover:bg-gray-50 transition-colors"
          >
            Cancel
          </button>
          <button
            @click="addSocial"
            class="px-6 py-3 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
          >
            Add Social
          </button>
        </div>
      </div>

      <!-- Gallery Upload Modal -->
      <div v-if="modalType === 'gallery'" class="p-6">
        <div class="w-full">
          <div class="p-4 border border-dashed border-primary/25 rounded-lg">
            <h4 class="mb-3 text-sm font-medium">Gallery Images</h4>
            <ul class="mb-2 text-xs text-gray-600">
              <li>999 KB limit.</li>
              <li>
                Allowed types: <span class="text-primary">JPG</span>,
                <span class="text-primary">JPEG</span>,
                <span class="text-primary">PNG</span>.
              </li>
            </ul>
            <div class="file-upload-container">
              <div class="file-upload-container-wrapper flex flex-wrap gap-4">
                <!--IMAGES PREVIEW-->
                <div
                  v-for="(image, index) in galleryImages"
                  :key="index"
                  class="file-upload-container-wrapper__preview relative"
                >
                  <img
                    :src="image.url"
                    class="w-24 h-24 object-cover rounded-lg"
                  />
                  <button
                    @click="removeMedia(index)"
                    class="absolute -top-2 -right-2 bg-red-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-xs hover:bg-red-600 transition-colors"
                    type="button"
                  >
                    <Icon name="material-symbols:close" />
                  </button>
                </div>
                <!--UPLOAD BUTTON-->
                <div class="file-upload-container-wrapper__add">
                  <label
                    for="gallery-file-input"
                    class="file-upload-container__add-btn w-24 h-24 border-2 border-dashed border-gray-300 rounded-lg flex items-center justify-center cursor-pointer hover:border-primary transition-colors"
                  >
                    <span>
                      <Icon
                        name="tabler:cloud-upload"
                        class="w-8 h-8 text-gray-400"
                      />
                    </span>
                  </label>
                  <input
                    @change="handleFileChange"
                    id="gallery-file-input"
                    type="file"
                    accept="image/*"
                    multiple
                    hidden
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="flex justify-end space-x-4 mt-6">
          <button
            @click="closeModal"
            class="px-6 py-3 border border-primary/25 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors"
          >
            Cancel
          </button>
          <button
            @click="uploadGallery"
            class="px-6 py-3 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
          >
            Upload Images
          </button>
        </div>
      </div>

      <!-- Video Modal -->
      <div v-if="modalType === 'video'" class="p-6">
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Video Title</label
            >
            <input
              v-model="newVideo.title"
              type="text"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >YouTube Video ID</label
            >
            <input
              v-model="newVideo.id"
              type="text"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
              placeholder="dQw4w9WgXcQ"
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Thumbnail URL</label
            >
            <input
              v-model="newVideo.thumbnail"
              type="url"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            />
          </div>
        </div>
        <div class="flex justify-end space-x-4 mt-6">
          <button
            @click="closeModal"
            class="px-6 py-3 border border-primary/25 text-primary rounded-lg hover:bg-gray-50 transition-colors"
          >
            Cancel
          </button>
          <button
            @click="addVideo"
            class="px-6 py-3 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
          >
            Add Video
          </button>
        </div>
      </div>

      <!-- Achievement Modal -->
      <div v-if="modalType === 'achievement'" class="p-6">
        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Achievement Title</label
            >
            <input
              v-model="newAchievement.title"
              type="text"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Year</label
            >
            <input
              v-model="newAchievement.year"
              type="number"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2"
              >Description</label
            >
            <input
              v-model="newAchievement.description"
              type="text"
              class="w-full px-4 py-3 rounded-lg border border-primary/25 focus:ring-2 focus:ring-primary focus:border-transparent transition"
            />
          </div>
        </div>
        <div class="flex justify-end space-x-4 mt-6">
          <button
            @click="closeModal"
            class="px-6 py-3 border border-primary/25 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors"
          >
            Cancel
          </button>
          <button
            @click="addAchievement"
            class="px-6 py-3 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors"
          >
            Add Achievement
          </button>
        </div>
      </div>
    </Modal>

    <!-- Image Modal -->
    <Modal2 :isOpen="imageModalOpen" @modal-close="closeImageModal">
      <div class="flex justify-center items-center p-4">
        <img
          :src="currentImageUrl"
          :alt="currentImageTitle"
          class="w-full max-w-3xl object-contain rounded-lg shadow-lg"
        />
      </div>
    </Modal2>

    <Modal2
      :isOpen="videoModalOpen"
      @modal-close="closeVideoModal"
      :title="currentVideoTitle"
    >
      <div class="flex justify-center items-center p-4">
        <div class="w-full aspect-video max-w-5xl">
          <iframe
            :src="currentVideoUrl"
            class="w-full h-full rounded-lg shadow-lg"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
      </div>
    </Modal2>
  </div>
</template>

<script setup>
// Celebrity data
const celebrity = ref({
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
    "https://images.unsplash.com/photo-1517841905240-472988babdf9?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1529626455594-4ff0802cfb7e?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1492681290082-e932832941e6?w=300&h=300&fit=crop",
    "https://images.unsplash.com/photo-1488426862026-3ee34a7d66df?w=300&h=300&fit=crop",
  ],
  videos: [
    {
      id: "https://www.youtube.com/embed/dQw4w9WgXcQ",
      title: "Priyotoma Official Trailer",
      views: "2.4M",
      duration: "2:45",
      thumbnail: "https://img.youtube.com/vi/dQw4w9WgXcQ/maxresdefault.jpg",
      uploadDate: "2023-10-15",
    },
    {
      id: "https://www.youtube.com/embed/9bZkp7q19f0",
      title: "Behind the Scenes - Nabab",
      views: "1.8M",
      duration: "5:32",
      thumbnail: "https://img.youtube.com/vi/9bZkp7q19f0/maxresdefault.jpg",
      uploadDate: "2022-08-22",
    },
    {
      id: "https://www.youtube.com/embed/J---aiyznGQ",
      title: "Interview with Sakib Khan",
      views: "3.1M",
      duration: "8:15",
      thumbnail: "https://img.youtube.com/vi/J---aiyznGQ/maxresdefault.jpg",
      uploadDate: "2023-05-10",
    },
  ],
});

// UI State
const activeTab = ref("overview");
const isModalOpened = ref(false);
const modalType = ref("");
const modalTitle = ref("");
const showProjectForm = ref(false);

// Image and Video Modal States
const imageModalOpen = ref(false);
const videoModalOpen = ref(false);
const currentImageUrl = ref("");
const currentImageTitle = ref("");
const currentVideoId = ref("");
const currentVideoTitle = ref("");

// Form data
const newProject = ref({
  title: "",
  year: new Date().getFullYear(),
  role: "",
  image: "",
  rating: 0,
  boxOffice: "",
});

const newSocial = ref({
  platform: "facebook",
  username: "",
});

const galleryImages = ref([]);

const newVideo = ref({
  title: "",
  id: "",
  thumbnail: "",
  views: "0",
  duration: "0:00",
  uploadDate: new Date().toISOString().split("T")[0],
});

const newAchievement = ref({
  title: "",
  year: new Date().getFullYear(),
  description: "",
  icon: "heroicons:trophy",
});

// Modal functions
const openModal = (type) => {
  modalType.value = type;
  isModalOpened.value = true;

  switch (type) {
    case "social":
      modalTitle.value = "Add Social Media";
      break;
    case "gallery":
      modalTitle.value = "Upload Gallery Images";
      break;
    case "video":
      modalTitle.value = "Add Video";
      break;
    case "achievement":
      modalTitle.value = "Add Achievement";
      break;
  }
};

const closeModal = () => {
  isModalOpened.value = false;
  modalType.value = "";
  modalTitle.value = "";
  // Reset form data
  newSocial.value = { platform: "facebook", username: "" };
  galleryImages.value = [];
  newVideo.value = {
    title: "",
    id: "",
    thumbnail: "",
    views: "0",
    duration: "0:00",
    uploadDate: new Date().toISOString().split("T")[0],
  };
  newAchievement.value = {
    title: "",
    year: new Date().getFullYear(),
    description: "",
    icon: "heroicons:trophy",
  };
};

// Image and Video Modal Functions
const openImageModal = (imageUrl, title) => {
  currentImageUrl.value = imageUrl;
  currentImageTitle.value = title;
  imageModalOpen.value = true;
};

const closeImageModal = () => {
  imageModalOpen.value = false;
  currentImageUrl.value = "";
  currentImageTitle.value = "";
};

const openVideoModal = (video) => {
  currentVideoUrl.value = video.id;
  currentVideoTitle.value = video.title;
  videoModalOpen.value = true;
};

const currentVideoUrl = ref("");

const closeVideoModal = () => {
  videoModalOpen.value = false;
  currentVideoId.value = "";
  currentVideoTitle.value = "";
};

const coverImg = ref(null);
const onCoverFileChange = (image) => {
  const file = image.target.files[0];
  newProject.value.cvrimage = file;
  coverImg.value = URL.createObjectURL(file);
};

// Handle multiple image upload
const handleFileChange = (event) => {
  for (let i = 0; i < event.target.files.length; i++) {
    galleryImages.value.push({
      url: URL.createObjectURL(event.target.files[i]),
      file: event.target.files[i],
    });
  }
};

const removeMedia = (index) => {
  galleryImages.value.splice(index, 1);
};

// Add functions
const addProject = () => {
  celebrity.value.recentProjects.push({
    ...newProject.value,
    image:
      newProject.value.image ||
      "https://images.unsplash.com/photo-1489599809505-7c8e1c869b38?w=400&h=300&fit=crop",
  });
  showProjectForm.value = false;
  newProject.value = {
    title: "",
    year: new Date().getFullYear(),
    role: "",
    image: "",
    rating: 0,
    boxOffice: "",
  };
};

const addSocial = () => {
  celebrity.value.socialMedia[newSocial.value.platform] =
    newSocial.value.username;
  closeModal();
};

const uploadGallery = () => {
  // In a real app, you would upload the files to a server
  // For demo, we'll just add the preview URLs
  galleryImages.value.forEach((image) => {
    celebrity.value.gallery.push(image.url);
  });
  closeModal();
};

const addVideo = () => {
  celebrity.value.videos.push({
    ...newVideo.value,
    thumbnail:
      newVideo.value.thumbnail ||
      "https://images.unsplash.com/photo-1489599809505-7c8e1c869b38?w=400&h=225&fit=crop",
  });
  closeModal();
};

const addAchievement = () => {
  celebrity.value.achievements.push({
    ...newAchievement.value,
  });
  closeModal();
};

// Helper functions
const getTabIcon = (tab) => {
  const icons = {
    overview: "heroicons:home",
    projects: "heroicons:film",
    gallery: "heroicons:photo",
    videos: "heroicons:play",
    achievements: "heroicons:trophy",
    "edit-profile": "heroicons:pencil-square",
  };
  return icons[tab] || "heroicons:document";
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

const saveProfile = () => {
  // Save profile implementation
  console.log("Saving profile:", celebrity.value);
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
</style>
