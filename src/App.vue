<template>
    <div id="app">
        <img src="@/assets/media/סמל קריית ההדרכה.png" class="logo" alt="Logo">
        <img v-if="page > 0" src="@/assets/media/gray triangle.png" alt="gray triangle" class="gray-triangle">
        <open-screen v-if="page === 0" @next-page="nextPage"></open-screen>
        <navbar v-if="page === 1" @next-page="nextPage"></navbar>
        <img src="@/assets/media/Artboard 74.png" alt="mador-till" class="mador-till">
    </div>
</template>

<script>

import OpenScreen from '@/components/OpenScreen.vue';
import Navbar from '@/components/Navbar.vue';

export default {
    name: "app",
    components: {
        OpenScreen,
        Navbar
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
    width: 5%;
    left: 0;
    top: 0;
    position: absolute;
    margin-top: 1%;
    margin-left: 1%;
    z-index: 3;
}

.mador-till {
    width: 5%;
    position: absolute;
    bottom: 0;
    right: 0;
    margin-bottom: 1%;
    margin-right: 1%;
    z-index: 3;
}

.gray-triangle {
    width: 13%;
    position: absolute;
    right: 0;
    bottom: 0;
}
</style> 

  