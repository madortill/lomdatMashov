<template>
    <div id="end-screen">
        <h3 class="conclusion-text">לסיכום</h3>
        <div class="finale-exe">
            <p v-for="(text, index) in array1" :key="text"
                :style="{'--delay': `${index * 3.2}s`,
                        '--width': `${text.length}ch`,
                         'font-size': index === 0 || index === 2 ? '3rem' : '1.6rem'}">
                {{ text }} </p>
        </div>
        <div v-show="showClose" class="finish-exe">
            <h1 class="finale-text">כל הכבוד סיימת את לומדת המשוב</h1>
            <button @click="closeWindow" class = "closeBtn">סיום</button>
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
                'החניך יעביר משוב אישי בצורה אפקטיבית.',
                'מטרות ביניים',
                'החניך יפרט עקרונות יסוד בשלב המשוב.',
                ' החניך יפרט את הכללים והמבנה הנכון של שיחת המשוב. ',
                'החניך יסביר את תהליך איתור מקורות אפשריים לתופעות במשוב.',
                'החניך יפרט את תהליך התמודדות עם התנגדויות במשוב.'
            ],
        };
    },
    mounted() {
        setTimeout(() => {
            this.showClose = true;
        }, 22000);
    },
    methods: {
        closeWindow() {
            window.close(); // סוגר את חלון האתר.
        },
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
    display: flex;
    justify-content: center;
    align-items: center;
}

.finale-text {
    color: white;
    font-size: 3.5rem;
}

.conclusion-text {
    color: #5f5a5a;
    font-size: 1.7rem;
}

@keyframes typeWrite {
    from {
        width: 0%;
    }

    to {
        width: var(--width);
    }
}

.finale-exe>p {
    display: block;
    width: fit-content;
    animation: typeWrite 2s var(--delay) steps(44) normal both, blink 500ms var(--delay) steps(45) 6;
    white-space: nowrap;
    text-align: right;
    overflow: hidden;
    border-left: solid 3px transparent;
    max-width: fit-content;
}


@keyframes blink {
    to {
        border-left-color: black;
    }

    from {
        border-left-color: transparent;
    }
}

.closeBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    font-size: 1.6rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #0492bd;
    min-width: 10%;
    height: 10%;
    top: 70%;
}

.closeBtn:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;

}
</style>
