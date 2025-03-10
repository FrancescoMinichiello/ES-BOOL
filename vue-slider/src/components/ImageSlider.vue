<script setup>
import { ref } from "vue";

const images = ref([
    "https://cdn.wallpapersafari.com/24/37/K4wNkq.jpg",
    "https://openmigration.org/wp-content/uploads/2021/02/G1A9815low-800x400.jpg",
    "https://best5.it/b5/wp-content/uploads/2021/06/Notre-Dame-de-Paris-1-800x400-1.jpg",
]);
</script>

<template>
    <div id="carouselExample" class="carousel slide custom-slider" data-bs-ride="carousel">
        <div class="carousel-inner">
            <div v-for="(image, index) in images" :key="index" class="carousel-item" :class="{ active: index === 0 }">
                <img :src="image" class="d-block w-100 rounded-3 shadow-lg" alt="Slide image" />
            </div>
        </div>
        <button class="carousel-control-prev custom-btn" type="button" data-bs-target="#carouselExample"
            data-bs-slide="prev">
            <span class="carousel-control-prev-icon"></span>
        </button>
        <button class="carousel-control-next custom-btn" type="button" data-bs-target="#carouselExample"
            data-bs-slide="next">
            <span class="carousel-control-next-icon"></span>
        </button>
    </div>
</template>

<style scoped>
.custom-slider {
    max-width: 700px;
    margin: 30px auto;
    border-radius: 15px;
    overflow: hidden;
}

.carousel-inner img {
    height: 400px;
    object-fit: cover;
    transition: transform 0.5s ease-in-out;
}

.carousel-item.active img {
    transform: scale(1.03);
}

.custom-btn {
    background-color: rgba(0, 0, 0, 0.5);
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.custom-btn:hover {
    background-color: rgba(0, 0, 0, 0.8);
}

.carousel-control-prev-icon,
.carousel-control-next-icon {
    width: 25px;
    height: 25px;
}
</style>