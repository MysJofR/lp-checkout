<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";

const menuItems = ref<string[]>([]);
const allItems = ["baas", "tech", "pay", "checkout", "sub"];

const ameiiLetters = ref<string[]>([]);
const payLetters = ref<string[]>([]);
const isScrolled = ref(false);

const handleScroll = () => {
  // Se rolou qualquer coisa (> 0), ativa o top-0
  isScrolled.value = window.scrollY > 0;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);

  setTimeout(() => {
    menuItems.value = allItems;
  }, 200);

  const ameiiText = "ameii".split("").reverse();
  ameiiText.forEach((letter, i) => {
    setTimeout(() => {
      ameiiLetters.value.unshift(letter);
    }, i * 100);
  });

  const payText = "pay".split("").reverse();
  payText.forEach((letter, i) => {
    setTimeout(() => {
      payLetters.value.unshift(letter);
    }, (ameiiText.length + i) * 100);
  });
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>

</template>

<style scoped>
.logo-slide-enter-active {
  transition: all 0.5s ease;
}
.logo-slide-enter-from {
  opacity: 0;
  transform: translateX(50px);
}
.logo-slide-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-in-enter-active {
  transition: all 0.5s ease;
}
.slide-in-enter-from {
  opacity: 0;
  transform: translateX(50px);
}
.slide-in-enter-to {
  opacity: 1;
  transform: translateX(0);
}
</style>
