<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

// troca a imagem se quiser um mock específico de integrações
import phoneMock from "/phone.png";

const phoneRef = ref<HTMLElement | null>(null);
const textRef = ref<HTMLElement | null>(null);

const phoneInView = ref(false);
const textInView = ref(false);

let observer: IntersectionObserver | null = null;

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.target === phoneRef.value) {
          phoneInView.value = entry.isIntersecting;
        }
        if (entry.target === textRef.value) {
          textInView.value = entry.isIntersecting;
        }
      });
    },
    {
      threshold: 0.25,
    }
  );

  if (phoneRef.value) observer.observe(phoneRef.value);
  if (textRef.value) observer.observe(textRef.value);
});

onBeforeUnmount(() => {
  if (!observer) return;
  if (phoneRef.value) observer.unobserve(phoneRef.value);
  if (textRef.value) observer.unobserve(textRef.value);
  observer.disconnect();
});
</script>

<template>
  <section class="w-full bg-[#F5F5F7] py-8">
    <div class="mx-auto max-w-5/6 bg-black p-4 sm:p-6 lg:p-8 lg:py-10 rounded-3xl">
      <div
        class="grid items-center gap-10 lg:gap-16 lg:grid-cols-[minmax(0,1.1fr)_minmax(0,1.1fr)]"
      >
        <!-- LADO ESQUERDO: PHONE / MOCK -->
        <div
          ref="phoneRef"
          class="flex justify-center lg:justify-center"
        >
          <div
            class="relative inline-flex rounded-[40px] b "
            :class="[
              'phone-anim',
              phoneInView ? 'phone-anim-in' : 'phone-anim-out',
            ]"
          >
            <img
              :src="phoneMock"
              alt="Integração Ameii Checkout com lojas online"
              class="w-[260px] sm:w-[300px] lg:w-[340px] h-full object-contain drop-shadow-2xl"
            />

            <!-- “card” flutuante sugerindo itens indo para o checkout -->
            <div
              class="hidden sm:block absolute -right-10 bottom-10 rounded-2xl bg-white/95 border border-[#E5E5EA] shadow-[0_14px_30px_rgba(0,0,0,0.12)] px-4 py-3 min-w-[190px]"
            >
              <p class="font-sf text-[11px] font-semibold text-[#6E6E73] mb-1">
                Carrinho sincronizado
              </p>
              <div class="space-y-1.5">
                <div class="flex items-center justify-between">
                  <span class="font-sf text-[11px] text-[#1D1D1F]">
                    Cadeira Office Pro
                  </span>
                  <span class="font-sf text-[11px] text-[#1D1D1F] font-semibold">
                    R$ 449,00
                  </span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="font-sf text-[11px] text-[#1D1D1F]">
                    Suporte ergonômico
                  </span>
                  <span class="font-sf text-[11px] text-[#1D1D1F] font-semibold">
                    R$ 89,00
                  </span>
                </div>
                <div class="mt-2 flex items-center justify-between border-t border-[#E5E5EA] pt-2">
                  <span class="font-sf text-[11px] text-[#6E6E73]">
                    Total
                  </span>
                  <span class="font-sf text-[12px] font-bold text-[#1D1D1F]">
                    R$ 538,00
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- LADO DIREITO: TEXTO -->
        <div
          ref="textRef"
          class="text-anim"
          :class="[
            textInView ? 'text-anim-in' : 'text-anim-out',
          ]"
        >
          <p
            class="font-sf text-xs sm:text-sm uppercase tracking-[0.26em] text-white/80 mb-3"
          >
            Integrações & Produtos
          </p>

          <h2
            class="font-sf text-[28px] sm:text-[34px] lg:text-[40px] font-bold leading-[1.1] text-white mb-4"
          >
            <span class="">Conecte</span>
            sua loja e deixe o
            <span class="text-[#FF1052]">checkout</span>
            fazer o resto.
          </h2>

          <p class="font-sf text-sm sm:text-[18px] text-white/80 leading-relaxed mb-4">
            Com integrações nativas para <img src="/shopify.png" class="w-4 mb-1 inline-flex" />  <span class="font-semibold text-[#87B344]  ">Shopify</span>
            e
            <span class="font-semibold font-sf   text-[#6E32CC]"> WooCommerce</span>,
            seus produtos, variações, preços e estoque vão direto para o Ameii
            Checkout — sem planilhas, plugins quebrados ou retrabalho.
          </p>

          <p class="font-sf text-sm sm:text-[18px] text-white/80 leading-relaxed mb-5">
            Seu cliente continua navegando na sua loja, mas quando decide comprar,
            encontra um checkout rápido, consistente e otimizado para conversão,
            com upsell, order bump e meios de pagamento avançados.
          </p>

          <ul class="space-y-2 mb-6 font-sf text-sm text-white/80">
            <li class="flex items-start gap-2">
              <span class="mt-[6px] inline-block h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span>Sincronização automática de catálogo, estoque e preços.</span>
            </li>
            <li class="flex items-start gap-2">
              <span class="mt-[6px] inline-block h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span>Suporte a múltiplas lojas, idiomas e moedas.</span>
            </li>
            <li class="flex items-start gap-2">
              <span class="mt-[6px] inline-block h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span>Produtos do Shopify/WooCommerce + recursos Ameii em um só fluxo.</span>
            </li>
          </ul>

          <div class="flex flex-wrap items-center gap-3">
            <button
              type="button"
              class="inline-flex items-center justify-center px-5 py-3 rounded-3xl bg-[#FF1052] text-white font-sf text-sm sm:text-base font-semibold  transition-all duration-200 hover:translate-y-[1px] "
            >
              Ver integrações disponíveis
            </button>

            <button
              type="button"
              class="inline-flex items-center justify-center px-4 py-2.5 rounded-3xl border border-[#D1D1D6] bg-white text-xs sm:text-sm font-sf text-[#1D1D1F] hover:bg-[#F5F5F7] transition-colors duration-150"
            >
                Saiba mais
            </button>
          </div>

           
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* PHONE: entra da esquerda, some pra esquerda. Reanima sempre que sai/entra */
.phone-anim {
  transition:
    opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
    transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  will-change: transform, opacity;
}

.phone-anim-out {
  opacity: 0;
  transform: translateX(-40px) scale(0.98);
}

.phone-anim-in {
  opacity: 1;
  transform: translateX(0) scale(1);
}

/* TEXTO: entra da direita, some pra direita */
.text-anim {
  transition:
    opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
    transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
  will-change: transform, opacity;
}

.text-anim-out {
  opacity: 0;
  transform: translateX(40px);
}

.text-anim-in {
  opacity: 1;
  transform: translateX(0);
}
</style>
