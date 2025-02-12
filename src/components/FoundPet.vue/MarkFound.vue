<script setup>
import { ref } from "vue";

const email = ref("");

function reload() {
    setTimeout(() => {
        window.location.reload();
    }, 500);

    const getEmail = JSON.parse(localStorage.getItem("pet_details")) || [];

    // it will filter email that don't match with what the user types.
    const filteredEmail = getEmail.filter(
        (userEmails) => userEmails.email !== email.value
    );


    // if the length of filtered email and get email is the same, it means nothing is filtered out. in other words, no email is found
    if (filteredEmail.length === getEmail.length) {
        alert("no email is found");
        return;
    }


    // setting new items based on filtered email. The matched email will be removed
    localStorage.setItem("pet_details", JSON.stringify(filteredEmail));
    alert("Yayy! We're happy your pet has been found!");
}
</script>

<template>
    <div class="absolute top-[50%] left-[50%] translate-[-50%] z-9999 bg-slate-200 w-fit border-2 rounded-md p-5"
        id="popup">
        <div class="w-[300px]">
            <h2 class="text-center text-2xl font-medium">Found Your Pet?</h2>
            <p class="text-center">Enter your email to mark as found</p>
            <form class="mt-5">
                <div class="mb-3">
                    <label class="text-lg font-medium text-[#2D2D2D]">Email:</label><br />
                    <input type="email" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" v-model="email" />
                </div>
                <div>
                    <a><button @click="reload"
                            class="py-2 px-3 cursor-pointer bg-[#3B82F6] rounded-md hover:bg-[#1E60D6] text-[#FFFFFF]"
                            type="button">
                            Submit
                        </button></a>
                </div>
            </form>
        </div>
        <span class="absolute top-0 right-2 font-extrabold cursor-pointer" @click="$emit('close')">X</span>
    </div>
</template>
