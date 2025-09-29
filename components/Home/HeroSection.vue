<script setup lang="ts">
const cars = [
  { name: "Sakib Khan", image: "/images/sakibKhan.jpg" },
  { name: "Shakib Al Hasan", image: "/images/ShakibAlHasan.jpeg" },
  { name: "Chanchal Chowdhury", image: "/images/chancal.jpg" },
  { name: "Dr.Muhammad Yunus", image: "/images/drYounus.jpg" },
  { name: "Sabila Nur", image: "/images/sabilanur.jpg" },
  { name: "Puja Cherry", image: "/images/pujaCherry.webp" },
  { name: "Mosharraf karim", image: "/images/mossharrof2.jpg" },
];

const activeIndex = ref<number | null>(null);

const getCarName = (carName: string, index: number) => {
  if (activeIndex.value === null) return carName;
  if (index === activeIndex.value) return carName;

  const words = carName.split(" ");
  return words.slice(0, 2).join(" ");
};
</script>

<template>
  <section class="w-full relative overflow-hidden">
    <div class="flex w-full h-auto">
      <div
        v-for="(car, index) in cars"
        :key="index"
        class="group relative h-full flex flex-col overflow-hidden transition-all duration-500 flex-1 hover:flex-[2] hover:z-10 min-w-0"
        @mouseenter="activeIndex = index"
        @mouseleave="activeIndex = null"
      >
        <!-- Car Image -->
        <div class="h-[550px] w-full overflow-hidden relative">
          <img
            :src="car.image"
            :alt="car.name"
            class="h-full w-full object-cover object-[10%_center] transition-all duration-500 ease-[cubic-bezier(0.25,0.1,0.25,1)] group-hover:object-[10%_center] group-hover:scale-[1.15] brightness-95 group-hover:brightness-100"
          />
        </div>

        <!-- Red Bar with Car Name -->
        <div
          class="bg-gradient-to-r from-tertiary to-primary text-white text-center py-3 text-sm md:text-base font-semibold tracking-wide transition-all duration-500 group-hover:py-5"
        >
          {{ getCarName(car.name, index) }}
        </div>
      </div>
    </div>
  </section>
</template>
