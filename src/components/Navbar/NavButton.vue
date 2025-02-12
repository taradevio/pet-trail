<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <RouterLink to="/foundpet"><button
            class="rounded-md p-3 cursor-pointer bg-[#3B82F6] text-[#FFFFFF] hover:bg-[#1E60D6]">Explore pets
            now!</button></RouterLink>
    <RouterLink to="/lostpet"><button
            class="rounded-md p-3 cursor-pointer bg-[#3B82F6] text-[#FFFFFF] hover:bg-[#1E60D6]">I
            want to report a lost pet!</button></RouterLink>
</template>