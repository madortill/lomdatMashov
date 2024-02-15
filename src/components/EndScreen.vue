<template>
    <div id="end-screen">
        <h3 class="conclusion-text">לסיכום</h3>
        <div class="finale-exe">
            <p v-for="(text, index) in array1" :key="text" :style="`--delay: ${index * 3.2}s`"> {{ text }} </p>
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
                'החניך יעביר משוב אישי בצורה אפקטיבית',
                'מטרות ביניים',
                'החניך יפרט עקרונות יסוד בשלב המשוב.',
                'חהניך יפרט את הכללים והמבנה הנכון של שיחת המשוב.',
                'החניך יסביר את תהליך איתור מקורות אפשריים לתופעות במשוב.',
                'החניך יפרט את תהליך התמודדות עם התנגדויות במשוב.'
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
    counter-reset: lines;
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
    padding: 0 2rem;
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

@keyframes typeWrite {
    from {
        width: 0%;
    }

    to {
        width: 100%;
    }
}

.finale-exe>p {
    display: block;
    width: fit-content;
    animation: typeWrite 3.2s var(--delay) steps(44) normal both, blink 500ms var(--delay) steps(45) 6;
    white-space: nowrap;
    text-align: right;
    overflow: hidden;
    border-left: solid 3px transparent;
}


@keyframes blink {
    to{
        border-left-color: black;
    }
    from {
        border-left-color: transparent;
    }
}</style>
