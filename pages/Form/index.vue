<script setup>
// Define celebrity categories with counts
const items = [
  { id: 1, title: "Footballers", icon: "mdi:soccer", count: "1.2K" },
  { id: 2, title: "Cricketers", icon: "mdi:cricket", count: "856" },
  { id: 3, title: "Actors", icon: "mdi:theater", count: "2.4K" },
  { id: 4, title: "Actress", icon: "mdi:account-star", count: "2.1K" },
  { id: 5, title: "Director", icon: "mdi:movie-open", count: "742" },
  { id: 6, title: "Influencers", icon: "mdi:instagram", count: "3.1K" },
  { id: 7, title: "Politicians", icon: "mdi:account-tie", count: "1.8K" },
  {
    id: 8,
    title: "Islamic Scholars",
    icon: "mdi:book-open-variant",
    count: "925",
  },
];

// Modal management
const isModalOpened = ref(false);
const selectedCategory = ref(null);
const currentPage = ref(1);

const form = ref({
  // Page 1
  name: "",
  image: null,
  cvrimage: null,
  heightFt: "",
  heightIn: "",
  weight: "",
  gender: "",
  birthday: "",
  starSign: "",

  // Page 2
  youtubeLink: "",
  linkedInLink: "",
  facebookLink: "",
  twitterLink: "",
  instagramLink: "",
  whatsapp: "",
  otherName: "",
  education: "",

  // Page 3
  email: "",
  phone: "",
  profession: "",
  religion: "",
  birthPlace: "",
  biography: "",
  categoryId: null,
});

const openModal = (category) => {
  selectedCategory.value = category;
  form.value.categoryId = category.id;
  currentPage.value = 1;
  isModalOpened.value = true;
};

const closeModal = () => {
  isModalOpened.value = false;
  selectedCategory.value = null;
  currentPage.value = 1;
  // Reset form
  Object.keys(form.value).forEach((key) => {
    if (key !== "categoryId") {
      form.value[key] = "";
    }
  });
  form.value.categoryId = null;
};

const nextPage = () => {
  if (validateCurrentPage()) {
    currentPage.value++;
  }
};

const prevPage = () => {
  currentPage.value--;
};

const skipToNext = () => {
  currentPage.value = 3; // Skip to the final page
};

const validateCurrentPage = () => {
  if (currentPage.value === 1) {
    if (!form.value.name || !form.value.gender || !form.value.birthday) {
      alert("Please fill all required fields (*)");
      return false;
    }
  } else if (currentPage.value === 3) {
    if (!form.value.email || !form.value.phone) {
      alert("Please fill all required fields (*)");
      return false;
    }
  }
  return true;
};

const profileImg = ref(null);
const onFileChange = (image) => {
  const file = image.target.files[0];
  form.value.image = file;
  profileImg.value = URL.createObjectURL(file);
};

const coverImg = ref(null);
const onCoverFileChange = (image) => {
  const file = image.target.files[0];
  form.value.cvrimage = file;
  coverImg.value = URL.createObjectURL(file);
};

const handleSubmit = () => {
  if (validateCurrentPage()) {
    // Submit form data
    console.log("Form submitted:", form.value);
    // Add your API call here
    alert("Application submitted successfully!");
    closeModal();
  }
};
</script>

<template>
  <!-- Header Banner -->
  <section
    class="relative h-[550px] bg-cover bg-top bg-no-repeat flex flex-col justify-center text-white py-20 overflow-hidden"
    style="background-image: url('/images/selector.png')"
  >
    <!-- Dark Overlay for better text readability -->
    <div class="absolute inset-0 bg-black/60"></div>
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
          Profile Submit
        </div>

        <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
          Select
          <span
            class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
            >Category</span
          >
        </h1>

        <!-- Added Subtitle -->
        <p
          class="text-xl md:text-2xl text-white/90 mb-8 leading-relaxed max-w-3xl mx-auto"
        >
          Choose your professional category to submit your profile and join our
          network of distinguished Bangladeshi personalities.
        </p>
      </div>
    </div>
  </section>

  <!-- Categories Section -->
  <section class="container mx-auto px-6 py-20">
    <div class="text-center mb-16">
      <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-4">
        Please Choose your
        <span
          class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary"
        >
          professional category
        </span>
      </h2>
    </div>
    <!-- Grid Container -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
      <div
        v-for="(item, index) in items"
        :key="index"
        class="group bg-white/80 backdrop-blur-sm rounded-2xl p-6 transition-all border border-primary duration-500 relative overflow-hidden h-full hover:shadow-2xl"
      >
        <!-- Corner accent -->
        <div
          class="absolute top-0 right-0 w-20 h-20 bg-gradient-to-bl from-blue-500/10 to-purple-500/10 rounded-bl-3xl transition-all duration-500 group-hover:from-blue-500/20 group-hover:to-purple-500/20"
        ></div>

        <!-- Icon Container -->
        <div class="relative z-10 mb-4">
          <div
            class="w-16 h-16 bg-gradient-to-br from-primary to-secondary rounded-2xl flex items-center justify-center shadow-lg group-hover:shadow-xl transition-all duration-500 group-hover:scale-110"
          >
            <Icon :name="item.icon" class="text-3xl text-white" />
          </div>
        </div>

        <!-- Content -->
        <div class="relative z-10">
          <h3
            class="font-bold text-xl text-gray-900 mb-3 group-hover:text-gray-800 transition-colors"
          >
            {{ item.title }}
          </h3>

          <div class="flex items-center mb-4">
            <div
              class="w-3 h-3 bg-green-500 rounded-full mr-3 animate-pulse shadow-lg"
            ></div>
            <span class="text-lg font-semibold text-gray-700"
              >{{ item.count }} Celebrities</span
            >
          </div>

          <p class="text-gray-600 text-sm leading-relaxed mb-6">
            Select {{ item.title.toLowerCase() }} category to submit your
            profile and join our network.
          </p>
        </div>

        <!-- Action Button -->
        <div class="relative z-10">
          <button
            @click="openModal(item)"
            class="group/btn w-full py-3 cursor-pointer bg-gradient-to-r border border-primary/15 from-primary to-secondary hover:from-secondary hover:to-primary rounded-xl text-white font-medium transition-all duration-500 shadow-md hover:shadow-xl transform hover:-translate-y-1"
          >
            <span class="flex items-center justify-center space-x-2">
              <span>Select</span>
            </span>
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- Modal -->
  <Modal
    :isOpen="isModalOpened"
    @modal-close="closeModal"
    :title="selectedCategory ? `Apply for ${selectedCategory.title}` : 'Apply'"
  >
    <div class="w-full">
      <!-- Progress Bar -->
      <div class="mb-8">
        <div class="flex items-center justify-between mb-2">
          <span class="text-sm font-medium text-gray-700"
            >Step {{ currentPage }} of 3</span
          >
          <span class="text-sm font-medium text-primary"
            >{{ Math.round((currentPage / 3) * 100) }}%</span
          >
        </div>
        <div class="w-full bg-gray-200 rounded-full h-2">
          <div
            class="bg-gradient-to-r from-primary to-secondary h-2 rounded-full transition-all duration-500 ease-out"
            :style="{ width: `${(currentPage / 3) * 100}%` }"
          ></div>
        </div>
      </div>

      <!-- Page 1: Basic Information -->
      <div v-if="currentPage === 1" class="space-y-6">
        <!-- Name & Image -->
        <div class="grid grid-cols-1 gap-6">
          <!-- Name -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:account-outline"
                class="w-4 h-4 mr-2 text-primary"
              />
              Full Name <span class="text-red-500 ml-1">*</span>
            </label>
            <div class="relative">
              <input
                v-model="form.name"
                type="text"
                placeholder="Enter your full name"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
                required
              />
              <Icon
                name="mdi:account"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
          <!-- Profile Image - 1/3 width -->
          <div class="space-y-2 lg:col-span-1">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:camera-outline"
                class="w-4 h-4 mr-2 text-primary"
              />
              Profile Image <span class="text-red-500 ml-1">*</span>
            </label>
            <label
              for="profile_image"
              class="block w-auto aspect-square max-h-64 flex items-center justify-center p-4 border-2 border-dashed border-primary/30 rounded-full text-primary cursor-pointer bg-gradient-to-br from-primary/5 to-secondary/5 hover:from-primary/10 hover:to-secondary/10 transition-all duration-300 group overflow-hidden"
            >
              <input
                type="file"
                id="profile_image"
                hidden
                @change="onFileChange"
              />
              <div v-if="!profileImg" class="text-center">
                <Icon
                  name="mdi:cloud-upload-outline"
                  class="w-8 h-8 mx-auto mb-2 text-primary group-hover:scale-110 transition-transform duration-300"
                />
                <p class="text-sm font-medium text-gray-700">Upload Profile</p>
                <p class="text-xs text-gray-500 mt-1">PNG, JPG, WEBP</p>
              </div>
              <div v-else class="relative w-full h-full">
                <img
                  :src="profileImg"
                  class="w-full h-full object-cover rounded-full shadow-md"
                />
                <div
                  class="absolute inset-0 bg-black/40 opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-full flex items-center justify-center"
                >
                  <Icon name="mdi:camera-plus" class="w-8 h-8 text-white" />
                </div>
              </div>
            </label>
          </div>

          <!-- Cover Image - 2/3 width -->
          <div class="space-y-2 lg:col-span-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
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
                  <Icon name="mdi:camera-plus" class="w-8 h-8 text-white" />
                </div>
              </div>
            </label>
          </div>
        </div>

        <!-- Height -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Height (Ft) -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:ruler" class="w-4 h-4 mr-2 text-primary" />
              Height (Feet)
            </label>
            <div class="relative">
              <select
                v-model="form.heightFt"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
              >
                <option value="">Select Feet</option>
                <option v-for="ft in 8" :key="ft" :value="ft">
                  {{ ft }} ft
                </option>
              </select>
              <Icon
                name="pixelarticons:human-height"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <Icon
                name="mdi:chevron-down"
                class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5 pointer-events-none"
              />
            </div>
          </div>

          <!-- Height (In) -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:ruler-square" class="w-4 h-4 mr-2 text-primary" />
              Height (Inches)
            </label>
            <div class="relative">
              <select
                v-model="form.heightIn"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
              >
                <option value="">Select Inches</option>
                <option v-for="inch in 12" :key="inch" :value="inch">
                  {{ inch }} in
                </option>
              </select>
              <Icon
                name="pixelarticons:human-height"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <Icon
                name="mdi:chevron-down"
                class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5 pointer-events-none"
              />
            </div>
          </div>
        </div>

        <!-- Weight & Gender -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Weight -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:weight-kilogram"
                class="w-4 h-4 mr-2 text-primary"
              />
              Weight
            </label>
            <div class="relative">
              <select
                v-model="form.weight"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
              >
                <option value="">Select Weight</option>
                <option v-for="kg in 150" :key="kg" :value="kg + 'kg'">
                  {{ kg }} kg
                </option>
              </select>
              <Icon
                name="hugeicons:body-weight"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <Icon
                name="mdi:chevron-down"
                class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5 pointer-events-none"
              />
            </div>
          </div>

          <!-- Gender -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:gender-male-female"
                class="w-4 h-4 mr-2 text-primary"
              />
              Gender <span class="text-red-500 ml-1">*</span>
            </label>
            <div class="relative">
              <select
                v-model="form.gender"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
                required
              >
                <option value="">Select Gender</option>
                <option value="male">Male</option>
                <option value="female">Female</option>
                <option value="other">Other</option>
              </select>
              <Icon
                name="ic:round-transgender"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <Icon
                name="mdi:chevron-down"
                class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5 pointer-events-none"
              />
            </div>
          </div>
        </div>

        <!-- Birthday & Star Sign -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Birthday -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:cake-variant" class="w-4 h-4 mr-2 text-primary" />
              Birthday <span class="text-red-500 ml-1">*</span>
            </label>
            <div class="relative">
              <input
                v-model="form.birthday"
                type="date"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary bg-white shadow-sm cursor-pointer"
                required
              />
              <Icon
                name="mdi:calendar"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Star Sign -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:star" class="w-4 h-4 mr-2 text-primary" />
              Star Sign
            </label>
            <div class="relative">
              <select
                v-model="form.starSign"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
              >
                <option value="">Select Star Sign</option>
                <option value="aries">Aries</option>
                <option value="taurus">Taurus</option>
                <option value="gemini">Gemini</option>
                <option value="cancer">Cancer</option>
                <option value="leo">Leo</option>
                <option value="virgo">Virgo</option>
                <option value="libra">Libra</option>
                <option value="scorpio">Scorpio</option>
                <option value="sagittarius">Sagittarius</option>
                <option value="capricorn">Capricorn</option>
                <option value="aquarius">Aquarius</option>
                <option value="pisces">Pisces</option>
              </select>
              <Icon
                name="mdi:zodiac-aries"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>
        </div>

        <!-- Navigation Buttons -->
        <div class="flex justify-between pt-6">
          <button
            @click="closeModal"
            class="flex items-center px-8 py-3 text-primary border border-primary/25 rounded-xl hover:bg-primary/35 hover:border-primary/25 transition-all duration-300 font-medium"
          >
            <Icon name="mdi:arrow-left" class="w-5 h-5 mr-2" />
            Cancel
          </button>
          <button
            @click="nextPage"
            class="flex items-center px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white rounded-xl hover:shadow-lg transform hover:-translate-y-0.5 transition-all duration-300 font-medium"
          >
            Continue
            <Icon name="mdi:arrow-right" class="w-5 h-5 ml-2" />
          </button>
        </div>
      </div>

      <!-- Page 2: Social Media & Education -->
      <div v-else-if="currentPage === 2" class="space-y-6">
        <!-- Social Media Links -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- YouTube -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:youtube" class="w-4 h-4 mr-2 text-red-600" />
              YouTube Channel
            </label>
            <div class="relative">
              <input
                v-model="form.youtubeLink"
                type="url"
                placeholder="https://youtube.com/yourchannel"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:play-circle"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Instagram -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:instagram" class="w-4 h-4 mr-2 text-pink-600" />
              Instagram Profile
            </label>
            <div class="relative">
              <input
                v-model="form.instagramLink"
                type="url"
                placeholder="https://instagram.com/username"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:image-filter"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- LinkedIn -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:linkedin" class="w-4 h-4 mr-2 text-blue-600" />
              LinkedIn Profile
            </label>
            <div class="relative">
              <input
                v-model="form.linkedInLink"
                type="url"
                placeholder="https://linkedin.com/in/username"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:briefcase"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Facebook -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:facebook" class="w-4 h-4 mr-2 text-blue-500" />
              Facebook Profile
            </label>
            <div class="relative">
              <input
                v-model="form.facebookLink"
                type="url"
                placeholder="https://facebook.com/username"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:account-box"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Twitter -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:twitter" class="w-4 h-4 mr-2 text-blue-400" />
              Twitter Profile
            </label>
            <div class="relative">
              <input
                v-model="form.twitterLink"
                type="url"
                placeholder="https://twitter.com/username"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:twitter"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- WhatsApp -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:whatsapp" class="w-4 h-4 mr-2 text-green-500" />
              WhatsApp Number
            </label>
            <div class="relative">
              <input
                v-model="form.whatsapp"
                type="tel"
                placeholder="+8801XXXXXXXXX"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:message-text"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>
        </div>

        <!-- Other Name & Education -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Other Name -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:card-account-details"
                class="w-4 h-4 mr-2 text-primary"
              />
              Other Name / Stage Name
            </label>
            <div class="relative">
              <input
                v-model="form.otherName"
                type="text"
                placeholder="Nickname or stage name"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:tag"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>
        </div>

        <!-- Education -->
        <div class="space-y-2">
          <label class="flex items-center text-sm font-medium text-gray-700">
            <Icon name="mdi:school" class="w-4 h-4 mr-2 text-primary" />
            Education
          </label>
          <div class="relative">
            <textarea
              v-model="form.education"
              placeholder="Your educational background"
              rows="3"
              class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm resize-none"
            ></textarea>
            <Icon
              name="mdi:book-education"
              class="absolute left-4 top-4 transform text-gray-400 w-5 h-5"
            />
          </div>
        </div>

        <!-- Navigation Buttons -->
        <div class="flex justify-between pt-6">
          <button
            @click="prevPage"
            class="flex items-center px-8 py-3 text-primary border border-primary/25 rounded-xl hover:bg-primary/35 hover:border-primary/25 transition-all duration-300 font-medium"
          >
            <Icon name="mdi:arrow-left" class="w-5 h-5 mr-2" />
            Previous
          </button>
          <div class="flex gap-3">
            <button
              @click="skipToNext"
              class="flex items-center px-8 py-3 text-yellow-900 border border-yellow-600 rounded-xl hover:bg-yellow-400 hover:border-yellow-600 transition-all duration-300 font-medium"
            >
              Skip this step
            </button>
            <button
              @click="nextPage"
              class="flex items-center px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white rounded-xl hover:shadow-lg transform hover:-translate-y-0.5 transition-all duration-300 font-medium"
            >
              Continue
              <Icon name="mdi:arrow-right" class="w-5 h-5 ml-2" />
            </button>
          </div>
        </div>
      </div>

      <!-- Page 3: Contact & Professional Details -->
      <div v-else-if="currentPage === 3" class="space-y-6">
        <!-- Email & Phone -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Email -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:email-outline"
                class="w-4 h-4 mr-2 text-primary"
              />
              Email Address <span class="text-red-500 ml-1">*</span>
            </label>
            <div class="relative">
              <input
                v-model="form.email"
                type="email"
                placeholder="your@email.com"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
                required
              />
              <Icon
                name="mdi:email"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Phone -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:phone-outline"
                class="w-4 h-4 mr-2 text-primary"
              />
              Phone Number <span class="text-red-500 ml-1">*</span>
            </label>
            <div class="relative">
              <input
                v-model="form.phone"
                type="tel"
                placeholder="+8801XXXXXXXXX"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
                required
              />
              <Icon
                name="mdi:phone"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>
        </div>

        <!-- Profession & Religion -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <!-- Profession -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon
                name="mdi:briefcase-outline"
                class="w-4 h-4 mr-2 text-primary"
              />
              Profession
            </label>
            <div class="relative">
              <input
                v-model="form.profession"
                type="text"
                placeholder="Your profession"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
              />
              <Icon
                name="mdi:briefcase"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
            </div>
          </div>

          <!-- Religion -->
          <div class="space-y-2">
            <label class="flex items-center text-sm font-medium text-gray-700">
              <Icon name="mdi:church" class="w-4 h-4 mr-2 text-primary" />
              Religion
            </label>
            <div class="relative">
              <select
                v-model="form.religion"
                class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary appearance-none bg-white shadow-sm cursor-pointer"
              >
                <option value="">Select Religion</option>
                <option value="islam">Islam</option>
                <option value="hinduism">Hinduism</option>
                <option value="christianity">Christianity</option>
                <option value="buddhism">Buddhism</option>
                <option value="other">Other</option>
              </select>
              <Icon
                name="streamline:religion-islam-religion-islam-moon-crescent-muslim-culture-star"
                class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
              />
              <Icon
                name="mdi:chevron-down"
                class="absolute right-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5 pointer-events-none"
              />
            </div>
          </div>
        </div>

        <!-- Birth Place -->
        <div class="space-y-2">
          <label class="flex items-center text-sm font-medium text-gray-700">
            <Icon
              name="mdi:map-marker-outline"
              class="w-4 h-4 mr-2 text-primary"
            />
            Birth Place
          </label>
          <div class="relative">
            <input
              v-model="form.birthPlace"
              type="text"
              placeholder="Where were you born?"
              class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm"
            />
            <Icon
              name="mdi:map-marker"
              class="absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5"
            />
          </div>
        </div>

        <!-- Biography -->
        <div class="space-y-2">
          <label class="flex items-center text-sm font-medium text-gray-700">
            <Icon
              name="mdi:card-account-details-outline"
              class="w-4 h-4 mr-2 text-primary"
            />
            Biography
          </label>
          <div class="relative">
            <textarea
              v-model="form.biography"
              placeholder="Tell us about yourself, your achievements, and your journey..."
              rows="4"
              class="w-full p-4 pl-11 border border-primary/25 rounded-xl focus:ring-2 focus:ring-primary/20 focus:border-primary transition-all duration-300 bg-white shadow-sm resize-none"
            ></textarea>
            <Icon
              name="mdi:lead-pencil"
              class="absolute left-4 top-4 transform text-gray-400 w-5 h-5"
            />
          </div>
        </div>

        <!-- Navigation Buttons -->
        <div class="flex justify-between pt-6">
          <button
            @click="prevPage"
            class="flex items-center px-8 py-3 text-primary border border-primary/25 rounded-xl hover:bg-primary/35 hover:border-primary/25 transition-all duration-300 font-medium"
          >
            <Icon name="mdi:arrow-left" class="w-5 h-5 mr-2" />
            Previous
          </button>
          <button
            @click="handleSubmit"
            class="flex items-center px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white rounded-xl hover:shadow-lg transform hover:-translate-y-0.5 transition-all duration-300 font-medium"
          >
            <Icon name="mdi:check" class="w-5 h-5 mr-2" />
            Submit Application
          </button>
        </div>
      </div>
    </div>
  </Modal>
</template>

<style scoped>
@keyframes pulse-slow {
  0%,
  100% {
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
