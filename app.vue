<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup>
const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
};
</script>

<style>
@import "tailwindcss";
@import "@nuxt/ui";
@theme {
  --color-primary: #6b1fad;
  --color-secondary: #ff3131;
  --color-tertiary: #1F2937;
}

/* Hide browser scrollbar completely */
::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for Firefox */
* {
  scrollbar-width: none;
}

/* Hide scrollbar for IE and Edge */
body {
  -ms-overflow-style: none;
}

/* Background pattern with subtle car elements */
body {
  position: relative;
}

body::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 20% 30%, rgba(139, 0, 0, 0.03) 1px, transparent 1px),
    radial-gradient(circle at 80% 70%, rgba(255, 0, 0, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  pointer-events: none;
  z-index: -1;
}
</style>