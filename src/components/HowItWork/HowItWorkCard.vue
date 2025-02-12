<script setup>
const steps = [
    {
        id: 1,
        title: 'Report',
        image:
            'https://images.pexels.com/photos/12911286/pexels-photo-12911286.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
        description: "Submit your pet's photo and last-seen location in 1 minute.",
        icon: '/pin.png',
    },
    {
        id: 2,
        title: 'Alert',
        image:
            'https://images.pexels.com/photos/193003/pexels-photo-193003.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
        description: 'We instantly alert neighbors, shelters, and local groups',
        icon: '/bell.png',
    },
    {
        id: 3,
        title: 'Reunite',
        image:
            'https://images.pexels.com/photos/30563640/pexels-photo-30563640/free-photo-of-joyful-child-with-a-baby-goat-in-bangladesh.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
        description: 'A bond never broken, just waiting to be found again.',
        icon: '/paw.png',
    },
]
</script>

<template>
    <div class="grid grid-cols-1 gap-7">
        <div v-for="step in steps" :key="step.id" class="mx-auto relative">
            <h3 class="text-lg md:text-xl font-medium text-center text-[#2D2D2D]">{{ step.title }}</h3>
            <div class="w-[350px] md:w-[500px] my-2">
                <img :src="step.image" class="w-full object-cover aspect-video rounded-md" />
            </div>
            <p class="w-[250px] md:w-[350px] text-lg md:text-xl text-center mx-auto text-[#555555]">
                {{ step.description }}
            </p>
            <div class="absolute top-5 -left-3">
                <img :src="step.icon" class="rounded-md" />
            </div>
        </div>
    </div>
</template>
