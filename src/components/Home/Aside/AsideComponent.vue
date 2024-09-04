<!-- AsideComponent.vue -->
<template>
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
</template>

<script setup>
import content from './content.json'

import { ref, onMounted, onBeforeUnmount } from 'vue'

const identityVisible = ref(false)

onMounted(() => {
    const handleScroll = () => {
        const asideElement = document.getElementById('aside')
        if (asideElement && asideElement.getBoundingClientRect().top <= 20) {
            identityVisible.value = true
        } else {
            identityVisible.value = false
        }
    }
    window.addEventListener('scroll', handleScroll)

    onBeforeUnmount(() => {
        window.removeEventListener('scroll', handleScroll)
    })
})

const getIconUrl = (iconPath) => {
    return `/svg/${iconPath}`
}

const getImageUrl = (imgPath) => {
    return `/img/${imgPath}`
}
</script>

<style scoped>
#aside .identity {
    flex-direction: column;
    justify-content: center;
    align-items: center;
    display: none;
    user-select: none;
}

#aside .identity.show {
    display: flex;
    animation: reveal 0.5s ease-in-out;
}

#aside img {
    border-radius: 50%;
    width: 100px;
}

#aside .name-title {
    text-align: center;
    margin-top: 20px;
}

#aside .name-title h2 {
    color: #fafafa;
    margin: 0 0 10px;
}

#aside .name-title p {
    color: #d6d6d6;
    margin: 0;
}

@keyframes reveal {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}

#aside .contacts-list {
    list-style: none;
    margin: 0;
    padding: 0;
}

#aside .contact-item {
    display: flex;
    align-items: center;
    margin: 20px 0;
}

#aside .icon-box {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    border: 1px solid rgba(85, 85, 85, 0.5);
    border-radius: 50%;
    margin-right: 10px;
}

#aside .svg-image {
    width: 30px;
    height: 100%;
}

#aside .contact-info {
    display: flex;
    flex-direction: column;
}

#aside .contact-title {
    margin: 0;
    font-size: 14px;
    font-weight: bold;
    color: #d6d6d6;
}

#aside .contact-link {
    margin: 5px 0 0 0;
    font-size: 16px;
    font-weight: bold;
    color: #fafafa;
    text-decoration: none;
}

#aside address {
    margin: 5px 0 0 0;
    font-size: 16px;
    font-weight: bold;
    color: #fafafa;
}

#aside .social-list {
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
    margin: 0;
    padding: 0;
}

#aside .social-item {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
}

#aside .social-item:not(:first-child):not(:last-child) {
    margin: 0 10px 0;
}

#aside .social-item .svg-image {
    width: 30px;
    height: 100%;
}

#aside .social-link {
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    padding: 5px;
    border-radius: 50%;
    transition: background-color 0.2s ease-in-out;
}

#aside .social-link:hover {
    background-color: #ffdb70;
}
</style>