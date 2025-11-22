<script setup lang="ts">
import phoneImg from "/phone.png"; // mock do app

// thumbs que vão ficar rodando em loop
const thumbs = [
  "/ameii-checkout.png",
  "/ameii-checkout.png",
  "/ameii-checkout.png",
  "/ameii-checkout.png",
  "/ameii-checkout.png",
  "/ameii-checkout.png",
];
</script>

<template>
  <section
    class="w-full bg-[#F5F5F7] flex justify-center   py-10  "
  >
    <!-- CARD PRINCIPAL -->
    <div
      class="w-full md:max-w-full   rounded-3xl sm:rounded-4xl    text-black overflow-hidden relative pb-[140px] sm:pb-40 lg:pb-[190px]"
    >
      <!-- CONTEÚDO PRINCIPAL -->
      <div
        class="relative max-w-5/6 mx-auto  flex flex-col lg:grid lg:grid-cols-3 gap-8 sm:gap-10 lg:gap-16 px-5 sm:px-8 lg:px-12 pt-8 sm:pt-12 lg:pt-16"
      >
        <!-- LADO ESQUERDO: PHONE -->
        <div class="flex  z-40 justify-center lg:justify-start">
          <div class="relative">
            <img
              :src="phoneImg"
              alt="Interface Ameii Hub"
              class="w-[180px]  sm:w-[220px] md:w-[260px] lg:w-[380px] h-auto object-cover  "
            />
          </div>
        </div>

        <!-- LADO DIREITO: TEXTO -->
        <div
          class="flex flex-col  mt-6 lg:mt-0 lg:col-span-2 max-w-xl lg:max-w-none"
        >
          <p
            class="font-sf text-[16px] sm:text-xs uppercase tracking-[0.25em] text-black/60 mb-3"
          >
            Ameii Hub Live
          </p>

          <h2
            class="font-sf text-xl sm:text-2xl md:text-3xl lg:text-[42px] font-bold leading-snug mb-3 sm:mb-4"
          >
            Sua operação na primeira fila de tudo o que acontece.
          </h2>

          <p
            class="font-sf text-sm sm:text-base md:text-[15px] lg:text-[20px] text-black/80"
          >
            Conecte
            <span class="text-[#FF1052] font-medium">Pay, Sub, BaaS, Tech e Checkout</span>
            em um só lugar e acompanhe a jornada completa — do clique ao saldo disponível.
            Aqui você conta com os melhores serviços para escalar sem medo!
            <br />
            <br />
            O ecossistema Ameii aumenta sua escala e diminui seus problemas.
          </p>
        </div>


        <div class="absolute z-10 w-5/6 lg:flex hidden bottom-5 right-0     h-40 ">
        <!-- gradiente pra “colar” no conteúdo acima -->
     

        <div class="absolute p-2 inset-0 overflow-hidden">
          <!-- trilha que se move infinito -->
          <div class="marquee-track">
            <!-- bloco 1 -->
            <div
              v-for="(thumb, idx) in thumbs"
              :key="'a-' + idx"
              class="marquee-item border border-[#D9D9D9]"
            >
              <img
                :src="thumb"
                alt=""
                class="h-full w-full object-cover"
              />
            </div>
            <!-- bloco 2 (duplicado) pra loop perfeito -->
            <div
              v-for="(thumb, idx) in thumbs"
              :key="'b-' + idx"
              class="marquee-item border border-[#D9D9D9] "
            >
              <img
                :src="thumb"
                alt=""
                class="h-full w-full object-cover"
              />
            </div>
          </div>
        </div>
      </div>
      </div>
      <div class="absolute z-10 w-full lg:hidden flex bottom-0 right-0     h-32 ">
        <!-- gradiente pra “colar” no conteúdo acima -->
     

        <div class="absolute p-2 inset-0 overflow-hidden">
          <!-- trilha que se move infinito -->
          <div class="marquee-track">
            <!-- bloco 1 -->
            <div
              v-for="(thumb, idx) in thumbs"
              :key="'a-' + idx"
              class="marquee-item border border-[#D9D9D9]"
            >
              <img
                :src="thumb"
                alt=""
                class="h-full w-full object-cover"
              />
            </div>
            <!-- bloco 2 (duplicado) pra loop perfeito -->
            <div
              v-for="(thumb, idx) in thumbs"
              :key="'b-' + idx"
              class="marquee-item border border-[#D9D9D9] "
            >
              <img
                :src="thumb"
                alt=""
                class="h-full w-full object-cover"
              />
            </div>
          </div>
        </div>
      </div>
      <!-- FAIXA DE IMAGENS EM LOOP (FUNDO INFERIOR) -->
     
    </div>
  </section>
</template>

<style scoped>
.marquee-track {
  display: flex;
  height: 100%;
  animation: marquee 35s linear infinite;
}

.marquee-item {
  flex: 0 0 220px;
  height: 100%;
  margin-right: 8px;
  border-radius: 8px;
  overflow: hidden;
}

/* mobile: cards um pouco menores */
@media (max-width: 640px) {
  .marquee-item {
    flex-basis: 170px;
    margin-right: 8px;
    border-radius: 6px;
  }
}

@keyframes marquee {
  0% {
    transform: translateX(0);
  }
  100% {
    /* como temos 2 blocos idênticos, 50% fecha o loop */
    transform: translateX(-50%);
  }
}
</style>
