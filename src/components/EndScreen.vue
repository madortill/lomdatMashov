<template>
    <div id="end-screen">
        <h3 class = "conclusion-text">לסיכום</h3>
        <div class="finale-exe">
            <h2>מטרות השיעור</h2>
            <h3>מטרת על</h3>
        </div>
        <div v-show="showClose" class="finish-exe">
            <h1 class="finale-text">כל הכבוד סיימת את לומדת המשוב</h1>
            <button @click="closeWindow">סיום</button>
        </div>
    </div>
</template>

<script>

export default {
    name: 'end-screen',
    components: {

    },
    data() {
        return {
            showClose: false,
            array1: [
                'מטרת על',
                'החניך יעביר משוב אישי בצורה אפקטיבית'
            ],
        };
    },
    mounted() {
        // setTimeout(() => {
        //     this.showClose = true;
        // }, 2000);
    },
    methods: {
        closeWindow() {
            // window.close(); // סוגר את חלון האתר.
        }
    },
}
</script>

<style>
#end-screen {
    background-color: #F2F2F2;
    width: 100%;
    height: 100vh;
    display: flex;
    position: relative;
    justify-content: center;
}

.finale-exe {
    position: absolute;
    width: 40%;
    height: 70%;
    left: 30%;
    bottom: 20%;
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
}

.finish-exe {
    position: absolute;
    width: 100%;
    height: 50%;
    text-align: center;
    background: #1F4E79;
    bottom: 30%;
}

.finale-text {
    color: white;
}

.conclusion-text {
    color: #5f5a5a;
    font-size: 1.2rem;
}

</style>
