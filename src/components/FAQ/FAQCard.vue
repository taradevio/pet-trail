<script setup>
import { ref } from "vue";
const FAQ = ref(null);

const faqs = [
    {
        id: 1,
        question: "Is this free?",
        answer:
            "Yes, this service is completely free to use. Our goal is to help reunite lost pets with their families without any cost.",
    },
    {
        id: 2,
        question: "How are alerts sent?",
        answer: "It will be sent through email",
    },
    {
        id: 3,
        question: "What if someone finds my pet?",
        answer:
            "If someone finds your pet, they can submit a found pet report on the app. You will receive an alert immediately.",
    },
    {
        id: 4,
        question: "How do I report a lost pet?",
        answer:
            "Simply click the 'Lost a Pet?' button, and you will be redirected directly to a form to fill in all the related information regarding your pet",
    },
    {
        id: 5,
        question: "How do I report a found pet?",
        answer:
            "Click the 'Found a Pet?'' button and you will be redirected to email",
    },
    {
        id: 6,
        question: "What should I do if I spot a pet but can't catch it?",
        answer:
            "You can report the sighting along with the location details. This will help the owner track their pet's last known location.",
    },
];

const toggleFaq = (id) => {
    // initially is set to null, so when clicked, the last condition will match. now, if the faq is equal to id, the condition is as shown below, meaning if we click the current faq or another faq, the current faq will be set to null, closing the faq. If we click another faq, the current faq will be set to null and the another faq will be set with id. try console logging FAQ. The param is passed to click event with arg of faq.id
    FAQ.value = FAQ.value === id ? null : id;
}
</script>

<template>
    <div class="mt-3 md:w-[650px] mx-auto">
        <div @click="toggleFaq(faq.id)" :key="faq.id" @close="FAQ" v-for="faq in faqs"
            class="border-b-1 py-2 px-2 mb-5 cursor-pointer border-[#F4A259]">
            <h3 class="mb-2 font-semibold md:text-xl text-[#2D2D2D]">{{ faq.question }}</h3>
            <div v-if="FAQ === faq.id">
                <p class="md:text-lg">{{ faq.answer }}</p>
            </div>
        </div>
    </div>
</template>
