<!-- HeroComponent.vue -->
<template>
    <div id="jumbotron">
        <div class="container">
            <div class="row">
                <div class="col-1" @click="nextProfileImage">
                    <img :src="currentProfileImage" alt="Profile Picture" id="profile-picture" />
                    <div class="overlay">
                        <span id="overlay-text">Next image</span>
                    </div>
                </div>
                <div class="col-2">
                    <h1>{{ content.profile.name }}</h1>
                    <p style="color: #ffdb70">{{ content.profile.title }}</p>
                    <p>{{ content.profile.description }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import content from './content.json'

const profileImages = ref([
    '/img/profil.webp',
    '/img/profil2.webp',
    '/img/profil3.webp',
    '/img/profil4.webp'
])
const profileImageIndex = ref(0)
const currentProfileImage = ref(profileImages.value[0])

const nextProfileImage = () => {
    profileImageIndex.value = (profileImageIndex.value + 1) % profileImages.value.length
    currentProfileImage.value = profileImages.value[profileImageIndex.value]
}

let profileImageInterval
onMounted(() => {
    profileImageInterval = setInterval(nextProfileImage, 10000)
})

onBeforeUnmount(() => {
    clearInterval(profileImageInterval)
})
</script>

<style scoped>
#jumbotron {
    padding: 5rem 0;
    margin-bottom: 0;
    color: #fafafa;
}

#jumbotron .container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
}

#jumbotron .row {
    display: flex;
    flex-wrap: wrap;
    margin: 0 auto;
    justify-content: center;
    align-items: center;
    gap: 50px;
}

#jumbotron .col-1 {
    flex-basis: 45%;
    position: relative;
}

#jumbotron .col-2 {
    flex-basis: 45%;
}

#jumbotron h1,
#jumbotron p {
    margin-top: 0;
}

#jumbotron p {
    font-size: 1.25rem;
    line-height: 1.5;
    margin-bottom: 1.25rem;
    color: #d6d6d6;
}

@media (max-width: 767px) {
    #jumbotron .container {
        max-width: 100%;
        padding-left: 15px;
        padding-right: 15px;
    }

    #jumbotron .col-1,
    #jumbotron .col-2 {
        flex-basis: 100%;
        text-align: center;
        margin-bottom: 2rem;
    }
}

#profile-picture {
    border-radius: 50%;
    max-width: 100%;
    height: auto;
}

.overlay {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.6);
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    transition: opacity 0.2s;
    cursor: pointer;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    -webkit-tap-highlight-color: transparent;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

.overlay:hover {
    opacity: 1;
}

#overlay-text {
    color: white;
    font-size: 24px;
    font-weight: bold;
    text-align: center;
}
</style>