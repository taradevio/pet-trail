<script setup>
import { onMounted, reactive } from "vue";
import L from 'leaflet'

onMounted(() => {
    const map = L.map("map").setView([0.7893, 113.9213], 14);
    L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 19,
        attribution:
            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    }).addTo(map);

    map
        .locate({
            enableHighAccuracy: true,
        })
        .on("locationfound", (e) => {
            const latlng = e.latlng;
            map.flyTo([latlng.lat, latlng.lng]);
        });

    const removeBtn = `<button id="remove" type="button" class="cursor-pointer font-semibold">Remove Marker?</button>`;

    function addMarker(e) {
        const newMarker = L.marker(e.latlng).addTo(map);
        const { _latlng } = newMarker;

        pet_details.lat = _latlng.lat;
        pet_details.lon = _latlng.lng;

        // remove marker
        newMarker.bindPopup(removeBtn);
        newMarker.on("popupopen", () => {
            document.getElementById("remove").addEventListener("click", () => {
                map.removeLayer(newMarker);
            });
        });
    }

    map.on("click", addMarker);
});

const pet_details = reactive({
    email: "",
    name: "",
    type: "",
    type_other: "",
    sex: "",
    breed: "",
    images: [],
    color: "",
    lat: null,
    lng: null,
    last_seen: "",
    add_details: "",
});

function handleImage(e) {
    if (!e.target.files.length) {
        alert("you must select images!");
        return;
    }

    // learn below further
    for (const file of e.target.files) {
        const reader = new FileReader();
        reader.readAsDataURL(file);

        reader.onload = (e) => {
            const img = new Image();
            img.src = e.target.result;

            img.onload = () => {
                const canvas = document.createElement("canvas");
                const ctx = canvas.getContext("2d");

                const maxWidth = 300;
                const maxHeight = 300;

                let width = img.width;
                let height = img.height;

                if (width > height) {
                    if (width > maxWidth) {
                        height *= maxWidth / width;
                        width = maxWidth;
                    }
                } else {
                    if (height > maxHeight) {
                        width *= maxHeight / height;
                        height = maxHeight;
                    }
                }

                canvas.width = width;
                canvas.height = height;
                ctx.drawImage(img, 0, 0, width, height);
                const compressImg = canvas.toDataURL("image/avif", 0.5);

                pet_details.images.push(compressImg);
            };
        };
    }
}

function submit() {
    let arr = JSON.parse(localStorage.getItem("pet_details") || "[]");

    const duplicateID = [];
    const setId = new Set();

    for (const petId of arr) {
        if (!setId.has(petId.id)) {
            setId.add(petId.id);
            duplicateID.push(petId);
        }
    }

    const id = duplicateID.length + 1;


    arr.push({ ...pet_details, id: id });

    if (
        !pet_details.email ||
        !pet_details.name ||
        !pet_details.breed ||
        !pet_details.color ||
        !pet_details.last_seen ||
        !pet_details.add_details
    ) {
        alert("You must fill in your pet information!");
        return;
    } else {
        setTimeout(() => {
            localStorage.setItem("pet_details", JSON.stringify(arr));
        }, 100);
        alert("we'll keep our fingers crossed!");
        window.location.reload();
    }
}
</script>

<template>
    <section class="mt-3 bg-[#FAFAFA]">
        <div class="md:grid place-content-center ps-3 pe-3">
            <h1 class="text-center text-4xl font-bold text-[#2D2D2D]">Report Your Lost Pet</h1>
            <form class="my-3 ">
                <div class="mb-3">
                    <label name="email" class="text-lg font-medium text-[#2D2D2D]">Email</label><br />
                    <input type="email" name="email" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" id="email"
                        v-model="pet_details.email" />
                </div>
                <div class="mb-5">
                    <label name="pet-name" class="text-lg font-medium text-[#2D2D2D]">Pet Name</label><br />
                    <input type="text" name="pet-name" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" id="name"
                        v-model="pet_details.name" />
                </div>
                <div class="mb-5">
                    <label name="pet-name" class="text-lg font-medium">Pet type</label><br />
                    <div class="inline-flex gap-2 items-center">
                        <input type="radio" id="dog" for="dog" name="pet_type" value="Dog" v-model="pet_details.type" />
                        <label for="dog">Dog</label><br />
                        <input type="radio" id="cat" for="dog" name="pet_type" value="Cat" v-model="pet_details.type" />
                        <label for="cat">Cat</label><br />
                        <label for="other">Other</label>
                        <input type="text" id="other" name="pet_type" class="border-[#D1D5DB] border-2 md:pl-2 w-full"
                            v-model="pet_details.type_other" />
                    </div>
                </div>
                <div class="mb-3">
                    <label class="text-lg font-medium">Pet Sex</label><br />
                    <div class="inline-flex gap-2 items-center">
                        <input type="radio" name="pet_sex" value="Male" v-model="pet_details.sex" />
                        <label for="male" id="male">Male</label><br />
                        <input type="radio" name="pet_sex" value="Female" v-model="pet_details.sex" />
                        <label for="female" id="female">Female</label><br />
                    </div>
                </div>

                <div class="mb-3">
                    <label name="pet-breed" class="text-lg font-medium">Pet Breed</label><br />
                    <input type="text" name="pet-breed" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" id="breed"
                        v-model="pet_details.breed" />
                </div>

                <div class="mb-3">
                    <label name="pet-color" class="text-lg font-medium">Pet Color</label><br />
                    <input type="text" name="pet-color" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" id="color"
                        v-model="pet_details.color" />
                </div>

                <div class="mb-3">
                    <label name="pet-images" class="text-lg font-medium">Pet Images</label><br />
                    <input type="file" name="images" id="images" class="border-[#D1D5DB] border-2 pl-2"
                        @change="handleImage" />
                </div>

                <div class="mb-3">
                    <label name="last-seen" class="text-lg font-medium">Last Seen</label><br />
                    <input type="text" name="last-seen" class="border-[#D1D5DB] border-2 py-2 pl-2 w-full" id="seen"
                        v-model="pet_details.last_seen" />
                </div>

                <div class="mb-3">
                    <label class="text-lg font-medium">Pinpoint Your Pet Location</label>
                    <div id="map" class="h-[450px] sm:w-[550px]"></div>
                </div>

                <div class="mb-3">
                    <label name="details" class="text-lg font-medium">Additional Details</label><br />
                    <textarea name="details" class="border-[#D1D5DB] border-2 w-full py-2 pl-2" id="details"
                        v-model="pet_details.add_details" rows="7" cols="45"></textarea>
                </div>
                <button @click="submit"
                    class="py-2 px-4 border-2 mt-3 cursor-pointer bg-[#3B82F6] text-[#FFFFFF] hover:bg-[#1E60D6] rounded-md">
                    Submit
                </button>
            </form>
        </div>
    </section>
</template>
