<template>
    <header>
        <h1 id="title">{{ content.title }}</h1>
        <nav id="nav">
            <ul>
                <li><a href="#">Portfolio</a></li>
                <li>
                    <a href="#" @click.prevent="toggleDropdown">
                        Services
                        <svg alt="dropdown" class="svg-drop" width="16px" viewBox="0 0 256 256"
                            xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M128,188a11.96187,11.96187,0,0,1-8.48535-3.51465l-80-80a12.0001,12.0001,0,0,1,16.9707-16.9707L128,159.0293l71.51465-71.51465a12.0001,12.0001,0,0,1,16.9707,16.9707l-80,80A11.96187,11.96187,0,0,1,128,188Z" />
                        </svg>
                    </a>
                    <ul v-if="dropdownVisible" class="dropdown">
                        <li><a href="#">Web Design</a></li>
                        <li><a href="#">Graphic Design</a></li>
                        <li><a href="#">Consultation</a></li>
                    </ul>
                </li>
                <li><a href="#">Contact</a></li>
            </ul>
        </nav>
    </header>

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

    <section id="skills">
        <div v-for="skill in content.skills" :key="skill.title" class="feature">
            <img :src="getIconUrl(skill.icon)" alt="Skill icon" class="svg-image" />
            <h3>{{ skill.title }}</h3>
            <p>{{ skill.description }}</p>
        </div>
    </section>

    <main id="main">
        <div id="content">
            <!-- Work Experiences Section -->
            <article class="article" title="Work Experiences">
                <ul>
                    <li v-for="experience in content.experiences" :key="experience.title" class="experience">
                        <h3>{{ experience.title }}</h3>
                        <p class="subline">{{ experience.company }} | {{ experience.date }}</p>
                        <ul>
                            <li v-for="desc in experience.description" :key="desc">{{ desc }}</li>
                        </ul>
                    </li>
                </ul>
            </article>

            <!-- Education Section -->
            <article class="article" title="Education Level">
                <ul>
                    <li v-for="education in content.education" :key="education.title" class="experience">
                        <h3>{{ education.title }}</h3>
                        <p class="subline">{{ education.institution }} | {{ education.date }}</p>
                        <ul>
                            <li v-for="desc in education.description" :key="desc">{{ desc }}</li>
                        </ul>
                    </li>
                </ul>
            </article>

            <!-- Organizational Experience Section -->
            <article class="article" title="Organizational Experience">
                <ul>
                    <li v-for="org in content.organizational" :key="org.title" class="experience">
                        <h3>{{ org.title }}</h3>
                        <p class="subline">{{ org.organization }} | {{ org.date }}</p>
                        <ul>
                            <li v-for="desc in org.description" :key="desc">{{ desc }}</li>
                        </ul>
                    </li>
                </ul>
            </article>

            <!-- Teaching Experience Section -->
            <article class="article" title="Teaching Experience">
                <ul>
                    <li v-for="teach in content.teaching" :key="teach.title" class="experience">
                        <h3>{{ teach.title }}</h3>
                        <p class="subline">{{ teach.institution }} | {{ teach.date }}</p>
                        <ul>
                            <li v-for="desc in teach.description" :key="desc">{{ desc }}</li>
                        </ul>
                    </li>
                </ul>
            </article>
        </div>

        <aside id="aside">
            <div class="card" name="identity">
                <div :class="['identity', { show: identityVisible }]">
                    <img :src="getImageUrl(content.profile.image)" alt="Identity Picture" id="identity-picture" />
                    <div class="name-title">
                        <h2>{{ content.profile.name }}</h2>
                        <p>{{ content.profile.title }}</p>
                    </div>
                </div>
                <ul class="contacts-list">
                    <li class="contact-item">
                        <div class="icon-box">
                            <img :src="getIconUrl('email.svg')" alt="Email" class="svg-image" />
                        </div>
                        <div class="contact-info">
                            <p class="contact-title">Email</p>
                            <a :href="'mailto:' + content.contact.email" class="contact-link">
                                {{ content.contact.email }}
                            </a>
                        </div>
                    </li>
                    <li class="contact-item">
                        <div class="icon-box">
                            <img :src="getIconUrl('phone.svg')" alt="Phone" class="svg-image" />
                        </div>
                        <div class="contact-info">
                            <p class="contact-title">Phone</p>
                            <a :href="'tel:' + content.contact.phone" class="contact-link">
                                {{ content.contact.phone }}
                            </a>
                        </div>
                    </li>
                    <li class="contact-item">
                        <div class="icon-box">
                            <img :src="getIconUrl('location.svg')" alt="Location" class="svg-image" />
                        </div>
                        <div class="contact-info">
                            <p class="contact-title">Location</p>
                            <address>{{ content.contact.location }}</address>
                        </div>
                    </li>
                </ul>
                <div class="separator"></div>
                <ul class="social-list">
                    <li class="social-item" title="LinkedIn">
                        <a :href="content.contact.social.linkedin" class="social-link">
                            <img :src="getIconUrl('linkedin.svg')" alt="LinkedIn" class="svg-image" />
                        </a>
                    </li>
                    <li class="social-item" title="Github">
                        <a :href="content.contact.social.github" class="social-link">
                            <img :src="getIconUrl('github.svg')" alt="Github" class="svg-image" />
                        </a>
                    </li>
                    <li class="social-item" title="Twitter">
                        <a :href="content.contact.social.twitter" class="social-link">
                            <img :src="getIconUrl('twitter.svg')" alt="Twitter" class="svg-image" />
                        </a>
                    </li>
                    <li class="social-item" title="Instagram">
                        <a :href="content.contact.social.instagram" class="social-link">
                            <img :src="getIconUrl('instagram.svg')" alt="Instagram" class="svg-image" />
                        </a>
                    </li>
                </ul>
            </div>
        </aside>
    </main>

    <footer>
        <p>&copy; 2023 Resume! - All rights reserved.</p>
    </footer>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import content from './content.json'

// Dropdown menu state
const dropdownVisible = ref(false)

// Function to toggle dropdown visibility for the "Services" menu
const toggleDropdown = () => {
    dropdownVisible.value = !dropdownVisible.value
}

// State for the profile image slider
const profileImages = ref([
    '/img/profil.webp',
    '/img/profil2.webp',
    '/img/profil3.webp',
    '/img/profil4.webp'
])
const profileImageIndex = ref(0)
const currentProfileImage = ref(profileImages.value[0])
const identityVisible = ref(false)

// Function to change profile image on overlay click
const nextProfileImage = () => {
    profileImageIndex.value = (profileImageIndex.value + 1) % profileImages.value.length
    currentProfileImage.value = profileImages.value[profileImageIndex.value]
}

// Auto change profile image every 10 seconds
let profileImageInterval
let scrollListener
onMounted(() => {
    // Image slider interval
    profileImageInterval = setInterval(() => {
        nextProfileImage()
    }, 10000)

    // Scroll event listener to reveal the identity section
    const handleScroll = () => {
        const asideElement = document.getElementById('aside')
        if (asideElement && asideElement.getBoundingClientRect().top <= 20) {
            identityVisible.value = true
        } else {
            identityVisible.value = false
        }
    }

    // Add the scroll event listener
    scrollListener = () => window.addEventListener('scroll', handleScroll)
    scrollListener()

    // Cleanup event listeners and intervals when component is unmounted
    onBeforeUnmount(() => {
        clearInterval(profileImageInterval)
        window.removeEventListener('scroll', handleScroll)
    })
})

// Get icon dynamically from public folder
const getIconUrl = (iconPath) => {
    return `/svg/${iconPath}`
}

// Get image dynamically from public folder
const getImageUrl = (imgPath) => {
    return `/img/${imgPath}`
}
</script>
