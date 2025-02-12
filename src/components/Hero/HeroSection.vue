<script setup>
import NavButton from '../Navbar/NavButton.vue';
</script>

<template>
    <section class="ps-5 pe-5 mt-6">
        <div class="lg:flex lg:items-center lg:justify-between">
            <div>
                <div class="text-center md:text-left">
                    <div class="lg:w-[600px] mx-auto">
                        <h1 class="text-3xl md:text-5xl font-bold mb-3 text-[#2D2D2D]">
                            Lost Your Pet? Alert Your Neighborhood in 60 Seconds
                        </h1>
                        <h2 class="text-xl mt-2 mb-6 text-[#555555] ">
                            Instantly notify nearby pet lovers, vet clinics, and shelters when
                            your pet goes missing.
                        </h2>
                    </div>
                </div>
                <div class="flex gap-3 mb-3 justify-center">
                    <NavButton />
                </div>
            </div>
            <div class="w-full md:w-[600px] lg:w-[700px] md:mx-auto">
                <img src="https://images.pexels.com/photos/28860760/pexels-photo-28860760/free-photo-of-man-interacting-with-bernese-mountain-dog-indoors.png?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
                    alt="pet image hero" class="object-cover lg:aspect-square" />
            </div>
        </div>
    </section>
</template>
