<!-- SkillsComponent.vue -->
<template>
    <section id="skills">
        <div v-for="skill in content.skills" :key="skill.title" class="feature">
            <img :src="getIconUrl(skill.icon)" alt="Skill icon" class="svg-image" />
            <h3>{{ skill.title }}</h3>
            <p>{{ skill.description }}</p>
        </div>
    </section>
</template>

<script setup>
import content from './content.json'

const getIconUrl = (iconPath) => {
    return `/svg/${iconPath}`
}
</script>

<style scoped>
#skills {
    background-color: #151515;
    border-top: #555 solid 1px;
    border-bottom: #555 solid 1px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    padding: 50px 0;
    color: #fafafa;
}

#skills .feature {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    margin: 0 20px;
    max-width: 300px;
}

#skills .feature .svg-image {
    width: 48px;
    height: 100%;
    margin-bottom: 5px;
}

#skills .feature h3 {
    font-size: 24px;
    margin-bottom: 10px;
}

#skills .feature p {
    font-size: 16px;
    margin-bottom: 20px;
    color: #d6d6d6;
}
</style>