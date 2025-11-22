<script setup lang="ts">
const pClasses =
  "text-white hover:underline underline-offset-2 text-lg font-sf font-bold";
const titleClasses = "text-gray-300 font-sf mb-4 font-bold";
</script>

<template>
  <footer class="bg-[#1D1D1F] relative px-6 py-16 sm:py-24">
    <div class="grid grid-cols-1 sticky top-0 lg:grid-cols-12 z-10 gap-8 lg:gap-12">
      <!-- (a parte de logo/descrição você pode adicionar aqui depois) -->

      <!-- Navigation Sections -->
      <div class="lg:col-span-8">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <!-- A Ameii Section -->
          <div class="flex flex-col gap-2">
            <h2 :class="titleClasses">Sobre a Ameii</h2>
            <nav class="flex flex-col gap-2">
              <a href="/" :class="pClasses">
                Início
              </a>
              <a href="/" :class="pClasses">
                Como funciona
              </a>
              <a href="/" :class="pClasses">
                Integrações
              </a>
              <a href="/" :class="pClasses">
                Recursos
              </a>
              <a href="/" :class="pClasses">
                Planos e Preços
              </a>
              <a href="/" :class="pClasses">
                Depoimentos
              </a>

            

             
            </nav>
          </div>

          <!-- SUPORTE Section -->
          <div class="flex flex-col gap-2">
            <h2 :class="titleClasses">SUPORTE</h2>
            <nav class="flex flex-col space-y-2">
              <a href="/" :class="pClasses">
                Central de Ajuda
              </a>
              <a href="/" :class="pClasses">
                Programa de Parcerias
              </a>
              <a href="/" :class="pClasses">
                Documentação da API
              </a>
            </nav>

            <h2 :class="titleClasses">POLÍTICAS</h2>
            <nav class="flex flex-col space-y-2">
              <a href="/" :class="pClasses">
                Termos de Uso
              </a>
              <a href="/" :class="pClasses">
                Políticas de Privacidade
              </a>
              <a href="/" :class="pClasses">
                Políticas de Cookies
              </a>
            </nav>
          </div>

          <!-- Terceira coluna vazia por enquanto (como no layout responsivo) -->
          <div class="hidden lg:block" />
        </div>
      </div>
    </div>

    <!-- SVG decorativo de fundo -->
    <div
      class="absolute w-full opacity-30 left-0 max-w-full bottom-0"
    >
      <svg viewBox="0 0 2000 482" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
          d="M1889.63 5V497H1821.7V5H1889.63Z"
          fill="#FF0152"
          stroke="#FF0152"
          stroke-width="10"
        />
        <path
          d="M1889.63 5V497H1821.7V5H1889.63Z"
          transform="translate(120, 0)"
          fill="#FF0152"
          stroke="#FF0152"
          stroke-width="10"
        />
        <path
          d="M1763.07 5V72.9297H1444.73V217.035H1737.19V284.965H1444.73V429.633H1769.81V497H1377.36V5H1763.07Z"
          fill="#FF0152"
          stroke="#FF0152"
          stroke-width="10"
        />
        <path
          d="M1273.69 5C1302.33 5 1325.37 28.0486 1325.37 56.6816V497H1258.01V90.9844L855.638 426.661L855.636 426.662C848.041 432.991 837.923 436.82 828.25 436.82C818.48 436.82 809 432.924 801.018 426.784L800.939 426.725L800.864 426.661L395.12 88.1729V497H327.752V58.9307C327.753 29.173 351.926 5 381.684 5C393.695 5.00011 405.671 9.06705 415.398 16.626L416.333 17.3682L416.358 17.3887L416.383 17.4102L828.25 361.19L1240.68 16.8477L1240.72 16.8145L1240.76 16.7822C1250.03 9.36486 1261.81 5.00003 1273.69 5Z"
          fill="#FF0152"
          stroke="#FF0152"
          stroke-width="10"
        />
        <path
          d="M53.3491 5C73.9241 5 92.6814 17.4717 100.194 36.8789L275.671 490.195L278.305 497H205.719L204.481 493.81L164.663 391.264H-57.9644L-97.7817 493.81L-99.021 497H-171.607L-168.973 490.195L6.50439 36.8789C14.0168 17.4718 32.7742 5.00004 53.3491 5ZM-31.5933 323.334H138.292L53.3491 103.724L-31.5933 323.334Z"
          fill="#FF0152"
          stroke="#FF0152"
          stroke-width="10"
        />
      </svg>
    </div>

    <!-- Copyright Section -->
    <div class="mt-12 pt-8">
      <div class="flex flex-col sm:flex-row sm:justify-between text-center sm:text-left">
        <p class="text-white text-sm">
          2025 © Todos os direitos reservados
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* nada extra aqui, tudo controlado via Tailwind */
</style>
