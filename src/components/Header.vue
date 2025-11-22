<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

const topMenu = ["Pagamentos", "Vendas", "Banking", "Tecnologia", "Suporte"];
const allItems = [
  {
    name: "AMEII PAY",
    img: "/icons/sub.svg",
  },
  {
    name: "Ameii Checkout",
    img: "/icons/checkout.svg",
  },
  {
    name: "Ameii BaaS",
    img: "/icons/baas.svg",
  },
  {
    name: "Ameii Tech",
    img: "/icons/tech.svg",
  },
  {
    name: "Ameii Sub",
    img: "/icons/pay.svg",
  },
];

const loaded = ref(false);
const mobileOpen = ref(false);
const showStickyBar = ref(false);

onMounted(() => {
  requestAnimationFrame(() => {
    loaded.value = true;
  });

  const handleScroll = () => {
    // quando passar um pouco do header de cima, ativa a barra fixa
    showStickyBar.value = window.scrollY > 80;
  };

  window.addEventListener("scroll", handleScroll, { passive: true });
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", () => {});
});

const toggleMobile = () => {
  mobileOpen.value = !mobileOpen.value;
};
</script>

<template>
  <header class="top-0 w-full border-b border-[#D1D1D3] bg-[#F5F5F7]">
    <!-- DESKTOP / TABLET -->
    <div class="hidden md:block max-h-[25vh]">
      <!-- PRIMEIRA BARRA (logo + menu) -->
      <div
        class="mx-auto max-w-3/6 flex flex-row justify-between gap-12 py-5 h-11 items-center"
      >
        <h1
          class="text-[#FF1052] w-fit text-[14px] cursor-pointer hover:text-[#FF1052]/80 font-extrabold font-mugesta header-item"
          :class="{ show: loaded }"
          style="animation-delay: 0.1s"
        >
          Ameii
        </h1>

        <span
          v-for="(item, i) in topMenu"
          :key="i"
          class="text-[12px] cursor-pointer hover:text-black font-sf text-black/80 header-item"
          :class="{ show: loaded }"
          :style="{ animationDelay: `${(i + 1) * 90}ms` }"
        >
          {{ item }}
        </span>

        <img
          src="@/assets/icons/search.svg"
          class="mt-0.5 h-9 header-item"
          :class="{ show: loaded }"
          style="animation-delay: 0.55s"
        />
      </div>

      <!-- SEGUNDA BARRA (AMEII CHECKOUT) – posição normal -->
      <div
        class="mx-auto max-w-3/6 flex flex-row justify-between gap-12 py-5 h-[52px] items-center transition-opacity duration-150"
        :class="showStickyBar ? 'opacity-0 pointer-events-none' : ''"
      >
        <h1
          class="text-[21px] font-sf font-semibold header-item"
          :class="{ show: loaded }"
          style="animation-delay: 0.1s"
        >
          Ameii Checkout
        </h1>

        <button
          type="button"
          class="px-3 py-1.5 cursor-pointer bg-[#FF1052] text-white rounded-2xl text-xs"
        >
          Acessar a plataforma
        </button>
      </div>
    </div>

    <!-- BARRA FIXA QUE APARECE AO ROLAR (somente DESKTOP) -->
    <div
      v-if="showStickyBar"
      class="hidden md:block fixed top-0 left-0 right-0 z-[100] border-b border-[#D1D1D3] bg-[#F5F5F7]/95 backdrop-blur"
    >
      <div
        class="mx-auto max-w-3/6 flex flex-row justify-between gap-12 py-3 h-[52px] items-center"
      >
        <h1 class="text-[19px] font-sf font-semibold">
          Ameii Checkout
        </h1>

        <button
          type="button"
          class="px-3 py-1.5 cursor-pointer bg-[#FF1052] text-white rounded-2xl text-xs"
        >
          Acessar a plataforma
        </button>
      </div>
    </div>

    <!-- MOBILE -->
    <div class="md:hidden border-b border-white/10">
      <!-- Barra principal -->
      <div class="flex items-center justify-between px-4 py-3">
        <h1 class="text-[#FF1052] text-[16px] font-extrabold font-mugesta">
          Ameii
        </h1>

        <div class="flex items-center gap-4">
          <img
            src="@/assets/icons/search.svg"
            class="h-8 w-8"
            alt="Buscar"
          />

          <!-- Botão hambúrguer -->
          <button
            type="button"
            class="relative flex flex-col justify-center gap-1 w-8 h-8 rounded-full bg-black/80 border border-white/10"
            @click="toggleMobile"
          >
            <span
              class="h-[2px] w-4 mx-auto rounded-full bg-white transition-transform"
              :class="mobileOpen ? 'translate-y-[3px] rotate-45' : ''"
            />
            <span
              class="h-[2px] w-4 mx-auto rounded-full bg-white transition-transform"
              :class="mobileOpen ? '-translate-y-[3px] -rotate-45' : ''"
            />
          </button>
        </div>
      </div>

      <!-- Menu mobile (se quiser depois é só completar aqui) -->
    </div>
  </header>
</template>

<style scoped>
.header-item,
.product-item {
  opacity: 0;
  transform: translateY(32px);
}

.header-item.show,
.product-item.show {
  animation: fadeSlideUp 1.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes fadeSlideUp {
  from {
    opacity: 0;
    transform: translateY(32px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* animação suave do menu mobile */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.25s ease-out;
}
.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}
</style>
