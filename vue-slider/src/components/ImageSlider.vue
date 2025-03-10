<script setup>
import { ref, onMounted, onUnmounted, nextTick } from "vue";
import { Carousel } from "bootstrap";

const images = ref([
    "https://cdn.wallpapersafari.com/24/37/K4wNkq.jpg",
    "https://openmigration.org/wp-content/uploads/2021/02/G1A9815low-800x400.jpg",
    "https://best5.it/b5/wp-content/uploads/2021/06/Notre-Dame-de-Paris-1-800x400-1.jpg",
]);

const currentIndex = ref(0);
const autoplay = ref(true);
let intervalId = null;
let carouselInstance = null;

onMounted(() => {
    nextTick(() => {
        const carouselElement = document.getElementById("carouselExample");
        if (carouselElement) {
            carouselInstance = new Carousel(carouselElement, {
                interval: false,
                ride: false,
            });
        }
    });

    if (autoplay.value) startAutoplay();
});

onUnmounted(() => {
    stopAutoplay();
});

const changeSlide = (index) => {
    if (carouselInstance) {
        carouselInstance.to(index);
        currentIndex.value = index;
    }
};

const nextSlide = () => {
    let newIndex = (currentIndex.value + 1) % images.value.length;
    changeSlide(newIndex);
};

const prevSlide = () => {
    let newIndex = (currentIndex.value - 1 + images.value.length) % images.value.length;
    changeSlide(newIndex);
};

const toggleAutoplay = () => {
    autoplay.value = !autoplay.value;
    if (autoplay.value) {
        startAutoplay();
    } else {
        stopAutoplay();
    }
};

const startAutoplay = () => {
    stopAutoplay();
    intervalId = setInterval(nextSlide, 5000);
};

const stopAutoplay = () => {
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }
};
</script>

<template>
    <div id="carouselExample" class="carousel slide custom-slider">
        <div class="carousel-inner">
            <div v-for="(image, index) in images" :key="index" class="carousel-item" :class="{ active: index === 0 }">
                <img :src="image" class="d-block w-100 rounded-3 shadow-lg" alt="Slide image" />
            </div>
        </div>

        <button class="carousel-control-prev custom-btn" type="button" @click="prevSlide">
            <span class="carousel-control-prev-icon"></span>
        </button>
        <button class="carousel-control-next custom-btn" type="button" @click="nextSlide">
            <span class="carousel-control-next-icon"></span>
        </button>

        <div class="thumbnails">
            <img v-for="(image, index) in images" :key="index" :src="image" class="thumbnail"
                :class="{ active: index === currentIndex }" @click="changeSlide(index)" />
        </div>

        <button @click="toggleAutoplay" class="btn btn-primary autoplay-btn">
            {{ autoplay ? "Stop Autoplay" : "Start Autoplay" }}
        </button>
    </div>
</template>

<style scoped>
.thumbnails {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 15px;
}

.thumbnail {
    width: 80px;
    height: 50px;
    object-fit: cover;
    border-radius: 5px;
    cursor: pointer;
    transition: transform 0.3s ease, border 0.3s ease;
}

.thumbnail:hover {
    transform: scale(1.1);
}

.thumbnail.active {
    border: 3px solid #007bff;
}

.autoplay-btn {
    display: block;
    margin: 15px auto;
    padding: 8px 16px;
    font-size: 16px;
    border: none;
    background: #007bff;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}

.autoplay-btn:hover {
    background: #0056b3;
}

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
