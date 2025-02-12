<script setup>
import { ref } from 'vue'

import MobileNav from './MobileNav.vue';
import NavButton from './NavButton.vue';
let navbar = ref(false)
</script>

<template>
  <header class="ps-5 pe-5 mt-3">
    <nav>
      <menu class="flex justify-between items-center border-1 rounded-md p-4 bg-[#FCE77D]">
        <a href="/">
          <div class="flex items-center gap-3">
            <img src="/pet-icon.png" alt="icon" />
            <h1 class="text-[#2D2D2D] text-2xl md:text-4xl font-bold">Pet Trail</h1>
          </div>
        </a>
        <div class="hidden lg:flex sm:gap-3">
          <NavButton />
        </div>
        <div class="block lg:hidden cursor-pointer" id="menu">
          <img src="/menu.svg" alt="hamburger menu" @click="navbar = !navbar" />
        </div>
      </menu>
    </nav>
    <MobileNav v-if="navbar" />
  </header>
</template>
