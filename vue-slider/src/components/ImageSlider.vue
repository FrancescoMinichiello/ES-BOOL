<script setup>
import { ref } from "vue";

const images = ref([
    "https://cdn.wallpapersafari.com/24/37/K4wNkq.jpg",
    "https://openmigration.org/wp-content/uploads/2021/02/G1A9815low-800x400.jpg",
    "https://best5.it/b5/wp-content/uploads/2021/06/Notre-Dame-de-Paris-1-800x400-1.jpg",
]);
</script>

<template>
    <div id="carouselExample" class="carousel slide w-75 mx-auto mt-5" data-bs-ride="carousel">
        <div class="carousel-inner">
            <div v-for="(image, index) in images" :key="index" class="carousel-item" :class="{ active: index === 0 }">
                <img :src="image" class="d-block w-100" alt="Slide image" />
            </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#carouselExample" data-bs-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#carouselExample" data-bs-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Next</span>
        </button>
    </div>
</template>