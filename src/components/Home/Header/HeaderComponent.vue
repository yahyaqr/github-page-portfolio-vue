<template>
    <header>
        <h1 id="title">{{ content.title }}</h1>
        <nav id="nav">
            <ul>
                <li v-for="(item, index) in content.nav.items" :key="item.name" class="nav-item">
                    <!-- Add a dynamic class 'active' to the parent a when the dropdown is visible -->
                    <a href="#" :class="{ active: activeDropdown === index }" @click.prevent="toggleDropdown(index)">
                        {{ item.name }}
                        <template v-if="item.subItems">
                            <svg alt="dropdown" class="svg-drop" width="16px" viewBox="0 0 256 256"
                                xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M128,188a11.96187,11.96187,0,0,1-8.48535-3.51465l-80-80a12.0001,12.0001,0,0,1,16.9707-16.9707L128,159.0293l71.51465-71.51465a12.0001,12.0001,0,0,1,16.9707,16.9707l-80,80A11.96187,11.96187,0,0,1,128,188Z" />
                            </svg>
                        </template>
                    </a>
                    <!-- Show dropdown when activeDropdown matches the index -->
                    <ul v-if="item.subItems && activeDropdown === index" class="dropdown">
                        <li v-for="subItem in item.subItems" :key="subItem.name">
                            <a :href="subItem.link">{{ subItem.name }}</a>
                        </li>
                    </ul>
                </li>
            </ul>
        </nav>
    </header>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import content from './content.json'

const activeDropdown = ref(null)

const toggleDropdown = (index) => {
    if (activeDropdown.value === index) {
        activeDropdown.value = null // Close the dropdown if it's already open
    } else {
        activeDropdown.value = index // Open the clicked dropdown
    }
}

// Close dropdown if click is outside the navigation
const handleClickOutside = (event) => {
    const nav = document.getElementById('nav')
    if (nav && !nav.contains(event.target)) {
        activeDropdown.value = null
    }
}

onMounted(() => {
    document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
    document.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped>
header {
    background-color: #151515;
    border-bottom: #555 solid 1px;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

#title {
    color: #ffdb70;
    cursor: pointer;
    user-select: none;
}

#title:hover {
    color: #fafafa;
}

#nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: space-between;
}

#nav li {
    position: relative;
}

#nav a {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px 20px;
    text-decoration: none;
    color: #d6d6d6;
}

#nav a:hover,
#nav a.active {
    color: #151515;
    background-color: #ffdb70;
}

#nav a:hover .svg-drop,
#nav a.active .svg-drop {
    fill: #151515;
}

#nav .svg-drop {
    margin-left: 8px;
    width: 16px;
    fill: #d6d6d6;
}

/* Dropdown styling */
#nav .dropdown {
    position: absolute;
    display: flex;
    flex-direction: column;
    top: 100%;
    left: 0;
    width: 200px;
    background-color: #ffdb70;
    z-index: 1;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

#nav .dropdown li {
    position: relative;
}

#nav .dropdown a {
    padding: 10px 20px;
    color: #151515;
    display: block;
    text-decoration: none;
}

#nav .dropdown a:hover {
    background-color: #ffcb2f;
    color: #151515;
}
</style>
