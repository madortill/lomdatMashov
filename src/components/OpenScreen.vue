<template>
    <div id="open-screen">
        <img src="@/assets/media/לוגו סופי לבן.png" alt="logo-white" class="logo-white">
        <h2 class="text-title">לומדת משוב</h2>
        <button class="btnNext" @click = "startTutorial"> התחל </button>
        <div class="animation-part">

        </div>
    </div>
</template>

<script>
export default {
    name: "open-screen",
    components: {

    },
    data() {
        return {

        };
    },
    methods: {
        startTutorial() {
            this.$emit('next-page');
        }
    },
};

</script>

<style scoped>
#open-screen {
    background-size: 100% 100%;
    direction: rtl;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #D9D9D9;
}

.logo-white {
    width: 30%;
}

.text-title {
    color: #A6A6A6;
    font-family: 'Heebo-Bold';
    font-size: xx-large;
    position: absolute;
    bottom: 25%;
    left: 25%;
}

.btnNext {
    background-color:#006998;
    position: absolute;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    cursor: pointer;   
    width: 9%;
    height: 6%;
    left: 10%;
    bottom: 13%;
    transition: background-color 0.3s linear;
}

.btnNext:hover {
    background-color: #00A4E6;
}

</style>