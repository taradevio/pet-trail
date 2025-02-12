<script setup>
import { RouterLink } from 'vue-router';

</script>

<template>
    <nav>
        <menu>
            <div class="lg:hidden sm:gap-3 border-1 rounded-md bg-[#FCE77D]">
                <RouterLink to="/foundpet">
                    <li class="py-2 px-4 text-[#2D2D2D] hover:bg-[#3B82F6]">Found a Pet?</li>
                </RouterLink>
                <RouterLink to="/lostpet">
                    <li class="py-2 px-4 text-[#2D2D2D] hover:bg-[#3B82F6]">Lost a Pet?</li>
                </RouterLink>
            </div>
        </menu>
    </nav>
</template>
