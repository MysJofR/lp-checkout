<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

const leftRef = ref<HTMLElement | null>(null);
const rightRef = ref<HTMLElement | null>(null);

const inViewLeft = ref(false);
const inViewRight = ref(false);

let observer: IntersectionObserver | null = null;

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.target === leftRef.value) {
          inViewLeft.value = entry.isIntersecting;
        }
        if (entry.target === rightRef.value) {
          inViewRight.value = entry.isIntersecting;
        }
      });
    },
    {
      threshold: 0.25, // começa a animar quando ~25% do bloco estiver visível
    }
  );

  if (leftRef.value) observer.observe(leftRef.value);
  if (rightRef.value) observer.observe(rightRef.value);
});

onBeforeUnmount(() => {
  if (observer) {
    if (leftRef.value) observer.unobserve(leftRef.value);
    if (rightRef.value) observer.unobserve(rightRef.value);
    observer.disconnect();
  }
});
</script>

<template>
  <section class="bg-[#F5F5F7] w-full  ">
    <div class="mx-auto bg-white max-w-5/6 p-4 rounded-3xl sm:p-6 lg:py-8">
      <div
        class="grid gap-6 lg:gap-10 lg:grid-cols-1 items-start"
      >
        <!-- COLUNA ESQUERDA: TEXTO -->
        <div
          ref="leftRef"
          class="anim-block-left col-span-2 text-center"
          :class="{ 'is-in-view-left': inViewLeft }"
        >
         
   

          <h1
            class="font-sf text-2xl sm:text-3xl  lg:text-[48px] font-bold text-[#1D1D1F] leading-snug mb-3"
          >
            Impulsione suas vendas com
            <br class="hidden sm:block" />
            um checkout de <span class="text-[#FF1052]">alta conversão</span>.
          </h1>

         
        </div>

        <!-- COLUNA DIREITA: MOCK DO CHECKOUT -->
        <div
          ref="rightRef"
          class="anim-block-right col-span-2  grid grid-cols-2"
          :class="{ 'is-in-view-right': inViewRight }"
        >

        <div class="flex flex-col px-10">

          <h1
            class="font-sf text-2xl sm:text-3xl  lg:text-[32px] font-bold text-[#1D1D1F] leading-snug mb-3"
          >
           Com o Checkout da Ameii
            <br class="hidden sm:block" />
            você prioriza a <span class="text-[#FF1052]">qualidade</span>.
          </h1>
          <p class="font-sf text-sm sm:text-[18px] text-black/80 leading-relaxed mb-6">
            Aumente seus lucros com o checkout otimizado da
            <span class="font-semibold text-[#1D1D1F]">Ameii</span> e garanta
            taxas competitivas, experiência fluida e uma jornada de pagamento
            que não deixa o cliente desistir no último passo.
          </p>

          <ul class="space-y-2 mb-8 text-black/80 text-sm font-sf">
            <li class="flex items-center gap-2">
              <span class="  h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span class="text-[16px]">Fluxo pensado para conversão em uma única tela.</span>
            </li>
            <li class="flex items-center   gap-2">
              <span class=" h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span class="text-[16px]">Suporte nativo a Pix, cartão e boletos no mesmo checkout.</span>
            </li>
            <li class="flex items-center gap-2">
              <span class=" h-1.5 w-1.5 rounded-full bg-[#FF1052]" />
              <span class="text-[16px]">Resumo claro do pedido, evitando dúvidas e abandono.</span>
            </li>
          </ul>

          <button
            type="button"
            class="inline-flex w-fit items-center justify-center px-5 py-3 rounded-3xl bg-[#FF1052] text-white font-sf text-sm sm:text-base font-semibold  transition-transform duration-200"
          >
            Começar agora
          </button>
        </div>


          <div
            class="rounded-3xl bg-white border border-[#E5E5EA] shadow-[0_18px_40px_rgba(0,0,0,0.06)] p-4 sm:p-5 lg:p-6 flex flex-col gap-4"
          >
            <div
              class="grid gap-4 lg:gap-5 lg:grid-cols-[minmax(0,1.2fr)_minmax(0,1fr)]"
            >
              <!-- MÉTODO DE PAGAMENTO -->
              <div
                class="rounded-2xl border border-[#E5E5EA] bg-[#F9F9FB] p-4 flex flex-col gap-3"
              >
                <p class="font-sf text-xs font-semibold text-[#6E6E73] mb-1">
                  Método de pagamento
                </p>

                <div class="grid grid-cols-2 gap-2 mb-2">
                  <button
                    type="button"
                    class="h-9 rounded-xl border border-[#FF1052] bg-white text-[11px] font-sf font-semibold text-[#FF1052] flex items-center justify-center gap-2 shadow-[0_0_0_1px_rgba(255,16,82,0.08)]"
                  >
               
                    Cartão de crédito
                  </button>

                  <button
                    type="button"
                    class="h-9 rounded-xl border border-[#D1D1D6] text-[11px] font-sf text-[#1D1D1F] flex items-center justify-center gap-2 bg-white hover:border-[#B0B0B5] transition"
                  >
                    
                    Pix
                  </button>
                </div>

                <div class="space-y-2">
                  <div>
                    <label
                      class="font-sf text-[11px] text-[#6E6E73] mb-1 block"
                    >
                      Número do cartão
                    </label>
                    <div
                      class="flex items-center gap-2 rounded-xl bg-white border border-[#D1D1D6] px-2.5 py-2"
                    >
                      <div class="flex gap-1">
                        <span
                          class="h-3 w-5 rounded-[6px] bg-gradient-to-r from-[#FF1052] to-[#00B3FF]"
                        ></span>
                        <span
                          class="h-3 w-5 rounded-[6px] bg-gradient-to-r from-[#FF1052] to-[#FF8A00]"
                        ></span>
                      </div>
                      <span
                        class="font-sf text-[11px] text-[#1D1D1F]/70 tracking-[0.18em]"
                      >
                        •••• •••• •••• 9123
                      </span>
                    </div>
                  </div>

                  <div class="grid grid-cols-2 gap-2">
                    <div>
                      <label
                        class="font-sf text-[11px] text-[#6E6E73] mb-1 block"
                      >
                        Vencimento
                      </label>
                      <div
                        class="rounded-xl bg-white border border-[#D1D1D6] px-2.5 py-2 text-[11px] text-[#1D1D1F]/70 font-sf"
                      >
                        10/27
                      </div>
                    </div>
                    <div>
                      <label
                        class="font-sf text-[11px] text-[#6E6E73] mb-1 block"
                      >
                        CVV
                      </label>
                      <div
                        class="rounded-xl bg-white border border-[#D1D1D6] px-2.5 py-2 text-[11px] text-[#1D1D1F]/70 font-sf text-right"
                      >
                        •••
                      </div>
                    </div>
                  </div>

                  <div>
                    <label
                      class="font-sf text-[11px] text-[#6E6E73] mb-1 block"
                    >
                      Nome no cartão
                    </label>
                    <div
                      class="rounded-xl bg-white border border-[#D1D1D6] px-2.5 py-2 text-[11px] text-[#1D1D1F]/80 font-sf"
                    >
                      Maria Oliveira
                    </div>
                  </div>
                </div>

                <button
                  type="button"
                  class="mt-3 h-10 w-full rounded-2xl bg-[#FF1052] text-white font-sf text-[12px] font-semibold flex items-center justify-center gap-2  hover:translate-y-[1px] transition-transform duration-200"
                >
                  Pagar R$ 499,00
                </button>
              </div>

              <!-- RESUMO -->
              <div
                class="rounded-2xl border border-[#E5E5EA] bg-white p-4 flex flex-col gap-3"
              >
                <p class="font-sf text-xs font-semibold text-[#6E6E73] mb-1">
                  Resumo
                </p>

                <div class="flex gap-3 items-center">
                  <div
                    class="h-10 w-10 rounded-xl bg-[#F5F5F7] flex items-center justify-center text-lg"
                  >
                    💺
                  </div>
                  <div class="flex-1">
                    <p
                      class="font-sf text-[12px] font-semibold text-[#1D1D1F]"
                    >
                      Cadeira de escritório Office Pro
                    </p>
                    <p class="font-sf text-[11px] text-[#6E6E73]">
                      Preto • 1 unidade
                    </p>
                  </div>
                  <p
                    class="font-sf text-[12px] font-semibold text-[#1D1D1F]"
                  >
                    R$ 449,00
                  </p>
                </div>

                <div
                  class="mt-2 flex items-center justify-between rounded-xl border border-dashed border-[#D1D1D6] px-3 py-2"
                >
                  <span class="font-sf text-[11px] text-[#6E6E73]">
                    Cupom de desconto
                  </span>
                  <button
                    type="button"
                    class="font-sf text-[11px] text-[#FF1052] font-semibold"
                  >
                    Aplicar
                  </button>
                </div>

                <div class="flex items-center justify-between mt-2">
                  <span class="font-sf text-[12px] text-[#6E6E73]">Total</span>
                  <span
                    class="font-sf text-[14px] font-bold text-[#1D1D1F]"
                  >
                    R$ 499,00
                  </span>
                </div>

                <div class="mt-3 pt-3 border-t border-[#E5E5EA]">
                  <p
                    class="font-sf text-[11px] text-[#6E6E73] mb-1 flex items-center gap-1"
                  >
                    <span
                      class="inline-flex h-4 w-4 items-center justify-center rounded-full bg-[#FF1052]/10 text-[10px]"
                    >
                      +
                    </span>
                    Oferta especial — Order Bump
                  </p>
                  <div
                    class="flex items-center justify-between rounded-xl bg-[#F5F5F7] px-3 py-2"
                  >
                    <div class="flex flex-col">
                      <span
                        class="font-sf text-[11px] text-[#1D1D1F] font-semibold"
                      >
                        Suporte ergonômico
                      </span>
                      <span class="font-sf text-[10px] text-[#6E6E73]">
                        + R$ 90,00
                      </span>
                    </div>
                    <label
                      class="relative inline-flex items-center cursor-pointer"
                    >
                      <input type="checkbox" class="sr-only peer" checked />
                      <span
                        class="w-8 h-4 bg-[#D1D1D6] peer-checked:bg-[#FF1052] rounded-full transition-colors duration-150"
                      ></span>
                      <span
                        class="absolute left-[3px] h-3 w-3 bg-white rounded-full shadow-sm peer-checked:translate-x-4 transition-transform duration-150"
                      ></span>
                    </label>
                  </div>
                </div>
              </div>
            </div>

            <!-- RODAPÉ DO MOCK -->
            <p class="mt-1 font-sf text-[10px] text-[#6E6E73] text-right">
              Tela ilustrativa do checkout Ameii. Valores fictícios.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* blocos animados – resetam sempre que entram/saem da viewport */
.anim-block-left,
.anim-block-right {
  opacity: 0;
  transform: translate3d(0, 12px, 0);
  transition:
    opacity 0.7s cubic-bezier(0.16, 1, 0.3, 1),
    transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
  will-change: opacity, transform;
}

.anim-block-left {
  transform: translate3d(-32px, 18px, 0);
}

.anim-block-right {
  transform: translate3d(32px, 18px, 0);
}

.anim-block-left.is-in-view-left,
.anim-block-right.is-in-view-right {
  opacity: 1;
  transform: translate3d(0, 0, 0);
}
</style>
