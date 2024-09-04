<!-- ExperienceComponent.vue -->
<template>
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
</template>

<script setup>
import content from './content.json'
</script>

<style scoped>
#content {
    flex: 1;
    margin-right: 20px;
}

#content .article {
    background-color: #151515;
    border: #555 solid 1px;
    border-radius: 20px;
    padding: 20px;
    margin-bottom: 20px;
    color: #d6d6d6;
}

.article ul li.experience {
    margin-top: 20px;
    cursor: help;
}

.article h2 {
    font-size: 24px;
    margin-bottom: 20px;
}

.article ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.article li {
    margin-bottom: 20px;
}

.article h3 {
    font-size: 18px;
    margin-bottom: 10px;
}

.article .experience:hover .subline {
    color: #ffdb70;
}

.article .subline {
    font-style: italic;
    color: #d6d6d680;
    margin-bottom: 10px;
}

.article ul li:first-child {
    margin-top: 0;
}

.article ul li:last-child {
    margin-bottom: 0;
}

.article ul ul {
    margin-left: 20px;
}

.article ul ul li {
    line-height: 1.7;
    margin-bottom: 10px;
}

.article ul ul li:last-child {
    margin-bottom: 0;
}
</style>