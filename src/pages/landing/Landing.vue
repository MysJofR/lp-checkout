
<script setup lang="ts">
import { ref, onMounted } from "vue";
import Header from "@/components/Header.vue";
import Headers from "@/components/Headers.vue";
import Start from "@/components/Start.vue";
import Services from "@/components/Services.vue";
import About from "@/components/About.vue";
import Footer from "@/components/Footer.vue";
import Products from "@/components/Products.vue";


</script>


<template>
    <div class="overflow-x-clip h-full">
    <div class="bg-[#010101] flex flex-col">
        <Header />
        <Start />
        <Services />
        <Products />
         
        <Footer />
        
      </div>
        <!-- <Services /> -->


    </div>
  
</template>


<style scoped>
    /* Logo: transição da direita pra esquerda */
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

    /* Itens do menu: mesmo estilo */
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

