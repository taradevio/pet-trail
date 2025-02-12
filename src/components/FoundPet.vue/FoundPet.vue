<script setup>
import { onMounted, ref } from "vue";
import L from "leaflet"
import MarkFound from "./MarkFound.vue";
const markPopup = ref(null);


onMounted(() => {
    const map = L.map("map").setView([0.7893, 113.9213], 14);
    map
        .locate({
            enableHighAccuracy: true,
        })
        .on("locationfound", (e) => {
            const latlng = e.latlng;
            map.flyTo([latlng.lat, latlng.lng]);
        });
    L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
        attribution:
            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    }).addTo(map);

    const getLatlng = localStorage.getItem("pet_details");
    const parseLatlng = getLatlng ? JSON.parse(getLatlng) : [];
    parseLatlng.forEach(({ lat, lon }) => {
        const eachMarker = L.marker([lat, lon]).addTo(map);

        // loop through and if the location matches, bind the popup. this will show image, depending on the location
        for (const petImages of parseObjs) {
            if (petImages.lat === lat && petImages.lon === lon) {
                eachMarker.bindPopup(`
        <div class="w-[200px]">
          <img src=${petImages.images} alt="image" class="w-full object-cover aspect-square">
          <p>Last seen: ${petImages.last_seen}</p>  
        </div>
      `);
            }
        }
    });
});

const items = localStorage.getItem("pet_details");

const parseObjs = JSON.parse(items) || [];

const sendEmail = (email) => {
    if (email) {
        window.location.href = `mailto:${email}`
    }
}
</script>

<template>
    <section class="bg-[#FAFAFA]">
        <div class="border-t-1 md:flex h-screen mt-3">
            <div class="w-full md:w-[40%] lg:w-[30%] ps-3 pe-3 overflow-auto">
                <div v-if="parseObjs.length === 0" class="content-center mt-5 md:mt-0 md:h-full">
                    <h2 class="text-center text-3xl">There are no lost pets</h2>
                </div>
                <div v-for="parseObj in parseObjs" v-else :key="parseObj.id"
                    class="my-2 border-b-2 border-[#D1D5DB] p-4 relative md:static">
                    <div class="mb-2">
                        <img v-for="image in parseObj.images" :src="image" :key="image.id"
                            class="w-[300px] aspect-square object-cover block mx-auto rounded-md" />
                    </div>
                    <div class="grid grid-cols-2">
                        <div class="mb-2">
                            <label class="font-bold">Name: </label>
                            <h1>{{ parseObj.name }}</h1>
                        </div>
                        <div class="mb-2">
                            <label class="font-bold">Type: </label>
                            <h1 class="border-1 px-2 rounded-lg w-max">
                                {{ parseObj.type || parseObj.type_other }}
                            </h1>
                        </div>
                        <div class="mb-2">
                            <label class="font-bold">Sex: </label>
                            <h1>{{ parseObj.sex }}</h1>
                        </div>
                        <div class="mb-2">
                            <label class="font-bold">Breed: </label>
                            <p>{{ parseObj.breed }}</p>
                        </div>
                        <div class="mb-2">
                            <label class="font-bold">Color: </label>
                            <p>{{ parseObj.color }}</p>
                        </div>
                        <div class="mb-2">
                            <label class="font-bold">Last Seen: </label>
                            <p>{{ parseObj.last_seen }}</p>
                        </div>
                        <div class="mb-2 col-span-2">
                            <label class="font-bold">Additional Details: </label>
                            <p>{{ parseObj.add_details }}</p>
                        </div>
                    </div>

                    <div class="inline-flex justify-center gap-3 w-full my-3">
                        <a @click="sendEmail(parseObj.email)" target="_blank"><button
                                class="py-2 px-3 cursor-pointer bg-[#3B82F6] rounded-md hover:bg-[#1E60D6] text-[#FFFFFF]">
                                Report to lost user
                            </button></a>
                        <button
                            class="py-2 px-3 cursor-pointer bg-[#3B82F6] rounded-md hover:bg-[#1E60D6] text-[#FFFFFF]"
                            @click="markPopup = parseObj.id">
                            Mark as found
                        </button>
                    </div>
                    <MarkFound v-if="markPopup === parseObj.id" @close="markPopup = false" />
                </div>
            </div>
            <div class="hidden md:block md:w-[60%] lg:w-[70%]" id="map"></div>
        </div>
    </section>
</template>
