<template>
    <div id="app">
        <img src="@/assets/media/mifkada-logo.png" class="logo" alt="Logo" @click = "homePage">
        <img v-if="page > 0" src="@/assets/media/graytriangle.png" alt="gray triangle" class="gray-triangle">
    
        <open-screen v-if="page === 0" @next-page="nextPage"></open-screen>
        <home-page  v-if="page === 1" @next-page="nextPage"></home-page>
        <end-screen v-if="page===2"></end-screen>
        
        <img src="@/assets/media/madortill.png" alt="mador-till" class="mador-till">
    </div>
</template>

<script>

import OpenScreen from '@/components/OpenScreen.vue';
import HomePage from '@/components/HomePage.vue';
import EndScreen from '@/components/EndScreen.vue';

export default {
    name: "app",
    components: {
        OpenScreen,
        HomePage,
        EndScreen,
    },
    data() {
        return {
            page: 0,
        };
    },
    methods: {
        nextPage() {
            this.page++;
        },
        prevPage() {
            this.page--;
        },
        homePage() {
            thispage === 1;
        }
    },
};

</script>

<style>
@font-face {
    font-family: 'Heebo';
    src: url('@/assets/fonts/heebo.regular.ttf');
}

@font-face {
    font-family: 'Heebo-Bold';
    src: url('@/assets/fonts/heebo.black.ttf');
}

* {
    overflow: hidden;
    font-family: 'Heebo';
}

body {
    margin: 0;
    direction: rtl;
}

#app {
    font-family: 'Heebo';
    width: 100vw;
    height: 100vh;
    position: relative;
}

.logo {
    max-width: 100px;
    left: 0;
    top: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}

.mador-till {
    /* min-width: 20px; */
    max-height: 10%;
    max-width: 90px;
    position: absolute;
    bottom: 0;
    right: 0;
    margin-bottom: 1%;
    margin-right: 1%;
    z-index: 3;
}

.gray-triangle {
    min-width: 50px;
    max-width: 220px;
    position: absolute;
    right: 0;
    bottom: 0;
    z-index: 2;
}
</style> 

  