<script setup>
import NavButton from '../Navbar/NavButton.vue';
</script>

<template>
    <footer class="mt-8">
        <div class="bg-[#FCE77D] p-3">
            <div class="flex items-center gap-3 justify-center">
                <img src="/pet-icon.png" alt="icon" />
                <h2 class="text-2xl text-[#2D2D2D]">Pet Trail</h2>
            </div>

            <div class="mt-5 mb-3 text-center inline-flex w-full gap-2 justify-center">
                <NavButton />
            </div>
            <div class="text-center">
                <p class="text-[#2D2D2D] font-semibold">&copy; 2025 Lost Pet Alert. Reuniting families since 2024</p>
            </div>
        </div>
    </footer>
</template>
