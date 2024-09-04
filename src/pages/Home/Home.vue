<template>
    <HeaderComponent />
    <HeroComponent />
    <SkillsComponent />

    <main id="main">
        <ContentComponent />

        <AsideComponent />
    </main>

    <footer>
        <p>&copy; 2023 Resume! - All rights reserved.</p>
    </footer>
</template>

<script setup>
import HeaderComponent from '../../components/Home/Header/HeaderComponent.vue'
import HeroComponent from '../../components/Home/Hero/HeroComponent.vue'
import SkillsComponent from '../../components/Home/Skills/SkillsComponent.vue'
import ContentComponent from '../../components/Home/Content/ContentComponent.vue'
import AsideComponent from '../../components/Home/Aside/AsideComponent.vue'
</script>

<style scoped>
#main {
    display: flex;
    padding: 20px;
    flex-wrap: wrap;
    justify-content: space-between;
}

#main .separator {
    margin: 25px auto 20px;
    width: 90%;
    height: 1px;
    background-color: #555;
}

#main aside {
    position: sticky;
    top: 20px;
    flex: 0 0 200px;
    height: 100%;
    background-color: #151515;
    border: #555 solid 1px;
    border-radius: 20px;
    padding: 20px;
    margin-bottom: 20px;
    color: #d6d6d6;
}

footer {
    background-color: #151515;
    border-top: #555 solid 1px;
    color: #fff;
    padding: 20px;
    text-align: center;
}

@media only screen and (max-width: 900px) {
    header {
        flex-direction: column;
        align-items: center;
    }

    #jumbotron #profile-picture,
    #jumbotron .overlay {
        max-width: 450px;
        margin: 0 auto;
    }

    main {
        flex-direction: column;
    }

    #content {
        margin-right: 0;
    }

    #main .aside {
        display: flex;
        flex: 0 0 100%;
    }

    #aside .identity {
        display: flex;
        animation: reveal 0.5s ease-in-out;
    }
}

@media only screen and (max-width: 600px) {
    #jumbotron .row {
        gap: 10px;
    }

    #jumbotron #profile-picture,
    #jumbotron .overlay {
        max-width: 350px;
        margin: 0 auto;
    }
}
</style>