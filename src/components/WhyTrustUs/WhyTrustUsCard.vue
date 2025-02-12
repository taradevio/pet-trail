<script setup>
import { ref } from 'vue'

const trustLists = [
    {
        id: 1,
        title: 'Quick & Hassle-Free Reporting',
        description:
            'Report your lost pet without any sign-up. Our concise form lets you share the essentials in under a minute—because every second counts when your pet is missing.',
        image:
            '/report.avif',
    },
    {
        id: 2,
        title: 'Explore Local Alerts with Interactive Mapping',
        description:
            "Browse active lost pet listings on our dedicated explore page and interactive map. Stay informed with alerts that focus solely on your pets' last-seen area, ensuring that help is always nearby.",
        image:
            '/foundpet.png',
    },
    {
        id: 3,
        title: 'Direct Connections & Effortless Updates',
        description:
            "When someone finds your pet, they're redirected straight to your email for seamless communication. Once your pet is back home, remove the listing with a single click to keep our community up-to-date.",
        image:
            '/email.webp',
    },
]
const img = ref(trustLists[0])

function hoverIn(image) {
    img.value = image
}
</script>

<template>
    <div class="md:flex md:items-center">
        <div class="mx-auto">
            <div v-for="trustlist in trustLists" :key="trustlist.id" class="mb-4 md:w-[600px] md:mx-auto">
                <h3 class="font-medium text-lg md:text-xl mb-1 text-[#2D2D2D] hover:text-[#F4A259]"
                    @mouseenter="hoverIn(trustlist)">
                    {{ trustlist.title }}
                </h3>
                <p class="md:text-md text-[#555555]">{{ trustlist.description }}</p>
            </div>
        </div>
        <!-- we use v-if give it an initial value, then since the func of hoverin passes an arg, the ref will have access to array of obj. Thus, the img src can be accessed from ref and pass the key of image from arr of obj -->
        <div class="hidden md:block md:ml-auto md:w-[500px]" v-if="img">
            <img :src="img.image" class="md:aspect-square md:object-cover md:w-full md:h-full" />
        </div>
    </div>
</template>
