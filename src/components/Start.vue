<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

const themes = [
  {
    label: "Lançamentos & infoprodutos",
    description:
      "Checkout enxuto, foco em conversão, timers, upsell e meios de pagamento pensados para alta demanda.",
    badge: "Para quem vende digital",
    color: "#FF1052",
  },
  {
    label: "Recorrência & assinaturas",
    description:
      "Perfeito para clubes, memberships e SaaS: planos, cobrança automática e experiência sem atrito.",
    badge: "Pagamentos recorrentes",
    color: "#FF1052",
  },
  {
    label: "E-commerce & produtos físicos",
    description:
      "Frete, endereço, dados completos e meios de pagamento flexíveis para quem envia todo dia.",
    badge: "Loja online",
    color: "#FF1052",
  },
  {
    label: "B2B & tickets altos",
    description:
      "Mais segurança, split de taxas, condições especiais e visão clara para time financeiro e comercial.",
    badge: "Operação robusta",
    color: "#FF1052",
  },
  {
    label: "Comunidades & clubes",
    description:
      "Acesso imediato, controle de status, cancelamento simples e experiência redonda para quem faz parte.",
    badge: "Engajamento contínuo",
    color: "#FF1052",
  },
];

// animação do hero (entra quando a página carrega)
const heroVisible = ref(false);

// animação dos cards (entra quando aparece no viewport)
const cardVisible = ref<boolean[]>(themes.map(() => false));
const cardRefs = ref<HTMLElement[]>([]);
let observer: IntersectionObserver | null = null;

onMounted(() => {
  // hero: pequena demora pra ficar mais suave
  requestAnimationFrame(() => {
    heroVisible.value = true;
  });

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const indexAttr = (entry.target as HTMLElement).dataset.index;
        if (!indexAttr) return;
        const index = Number(indexAttr);
        if (entry.isIntersecting) {
          cardVisible.value[index] = true;
          observer?.unobserve(entry.target); // não precisa observar mais depois de animar
        }
      });
    },
    {
      threshold: 0.2,
    }
  );

  // começa a observar cada card
  cardRefs.value.forEach((el) => {
    if (el) observer?.observe(el);
  });
});

onBeforeUnmount(() => {
  observer?.disconnect();
});
</script>

<template>
  <div class="bg-[#F5F5F7]  w-full py-8 pt-20 h-full">
    <!-- HERO -->
    <div
      class="mx-auto items-center flex flex-col gap-8 max-w-3/6 px-4"
      :class="[
        'transition-all duration-700 ease-[cubic-bezier(0.16,1,0.3,1)]',
        heroVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-6'
      ]"
    >
      <div
        class="flex flex-col justify-center gap-4 items-center"
      >
        <img
          src="/icons/checkout.svg"
          class="w-20 bg-[#FF1052] p-2 rounded-2xl shadow-2xl"
        />
        <h1
          class="font-sf text-center font-semibold text-[#1d1d1f] text-sm"
        >
          Ameii Checkout
        </h1>
      </div>

      <h1
        class="font-sf text-center leading-18 text-[#1d1d1f] font-bold text-[40px] sm:text-[56px] lg:text-[72px]"
      >
        Uma infinidade <br />
        de temas para seu interesse não ter fim.
      </h1>

      <p
        class="font-sf text-center leading-tight text-[#1d1d1f] text-base sm:text-lg lg:text-[21px] max-w-3xl"
      >
        Explore jornadas de checkout pensadas para cada tipo de operação.
        <br class="hidden sm:block" />
        Da primeira venda ao scale-up, a Ameii entrega a experiência certa para
        o seu cliente — e controle total para o seu time.
      </p>

      <button
        type="button"
        class="px-5 w-fit py-3 cursor-pointer bg-[#FF1052] text-white rounded-3xl text-lg font-sf transition-all duration-300 ease-out hover:-translate-y-0.5 hover:shadow-xl hover:bg-[#ff1e64]"
      >
        Acessar a plataforma
      </button>
    </div>

    <!-- SEÇÃO DE “TEMAS” DO CHECKOUT -->
    <div class="mt-20 mx-auto px-4 sm:px-6">
      <div
        class="text-center mb-10 transition-all duration-700 ease-[cubic-bezier(0.16,1,0.3,1)]"
        :class="heroVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
        style="transition-delay: 120ms"
      >
        <h2
          class="mt-3 font-sf text-2xl sm:text-3xl font-bold text-[#1D1D1F]"
        >
          Um checkout que se adapta ao seu jeito de vender.
        </h2>
        <p class="mt-2 font-sf text-sm sm:text-base text-black/80">
          Escolha o tipo de operação e customize tudo: layout, etapas,
          pagamentos e comunicações.
        </p>
      </div>

      <!-- CARDS / “TELAS” DE CHECKOUT -->
      <div
        class="grid gap-5 sm:gap-6 md:grid-cols-5 lg:grid-cols-5 auto-rows-fr"
      >
        <div
          v-for="(theme, index) in themes"
          :key="index"
          :data-index="index"
          :ref="(el) => (cardRefs[index] = el as HTMLElement)"
          class="group relative overflow-hidden rounded-3xl bg-white shadow-inner backdrop-blur-3xl border border-[#E5E5EA] flex flex-col justify-between p-4 sm:p-5 transition-all duration-700 ease-[cubic-bezier(0.16,1,0.3,1)]"
          :class="cardVisible[index]
            ? 'opacity-100 translate-x-0 translate-y-0'
            : 'opacity-0 translate-x-6 translate-y-6'"
          :style="{ transitionDelay: (index * 90) + 'ms' }"
        >
        

          <div class="space-y-3">
            <span
              class="inline-flex rounded-full px-3 py-1 text-[10px] font-sf font-semibold tracking-[0.16em] uppercase"
              :style="{
                backgroundColor: theme.color + '15',
                color: theme.color,
              }"
            >
              {{ theme.badge }}
            </span>

            <h3
              class="font-sf text-base sm:text-lg font-semibold text-[#1D1D1F]"
            >
              {{ theme.label }}
            </h3>

            <p class="font-sf text-xs sm:text-sm text-[#515154] leading-snug">
              {{ theme.description }}
            </p>
          </div>

          <!-- preview do checkout -->
          <img src="/ameii-checkout.png" alt="" class="mt-4 rounded-2xl" />
        </div>
      </div>

      <!-- CTA secundária embaixo dos cards -->
      <div
        class="mt-10 text-center transition-all duration-700 ease-[cubic-bezier(0.16,1,0.3,1)]"
        :class="heroVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'"
        style="transition-delay: 200ms"
      >
        <p class="font-sf text-xs sm:text-sm text-black/80">
          Não encontrou seu modelo ideal?
        </p>
        <button
          type="button"
          class="mt-2 px-4 py-2 rounded-3xl border border-[#D1D1D6] text-xs sm:text-sm font-sf text-[#1D1D1F] bg-white hover:bg-[#F5F5F7] hover:-translate-y-0.5 hover:shadow-md transition-all duration-300"
        >
          Acesse a plataforma e estilize seu checkout da forma que desejar
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* nada extra aqui – tudo feito com Tailwind + classes conditionais */
</style>
