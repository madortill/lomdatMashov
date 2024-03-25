<template>
    <div id="video-information">
        <h2 class="obj-title">{{ objections[indexObjection].title }}</h2>
        <p class="obj-text"> {{ objections[indexObjection].info }}</p>
        <button class="nextBtnVideo" @click="nextVideo">המשך</button>
    </div>
</template>

<script>
export default {
    name: 'video-information',
    props: ['indexObjection'],
    data() {
        return {
            objections: [
                {
                    title: 'המסכים לכאורה',
                    info: 'מחכה לתשובת החונך ומיד מסכים איתו ומנסה להעביר את השיחה במהירות האפשרית.',
                },
                {
                    title: 'היהיר',
                    info: 'מלגלג מזלזל ועוקצני. בדרך כלל גם עלול להעליב ולא מוכן לקבל הערות לשיפור.',
                },
                {
                    title: 'הטראגי',
                    info: 'חסר פרופורציות. בוכה לעיתים וחש בתחושת כישלון גמור.',
                },
                {
                    title: 'הווכחן',
                    info: 'לא מסכים עם אף נקודה. משתלט על השיחה ומרים את קולו.',
                },
            ],
        }
    },
    methods: {
        nextVideo() {
            setTimeout(() => {
                this.$emit('next-video');
            }, 500);

        }
    },
}

</script>

<style>
.nextBtnVideo {
    background-color: #029cd9;
    /* margin: 0 2rem; */
    cursor: pointer;
    border: none;
    font-size: 1.2rem;
    color: #ffffff;
    border-radius: 100px;
    padding: 10px 20px;
    transition: background-color 0.3s ease;
    /* position: absolute; */
    /* margin-left: 5%; */
}

.nextBtnVideo:hover {
    animation: borderPulse 4000ms infinite ease-out, hoverShine 200ms, pulse 0.5s infinite alternate;
}

@keyframes pulse {
    0% {
        background-color: #047fb0;
    }

    100% {
        background-color: #105a7f;
    }
}

.obj-text {
    font-size: 1.4rem;
}

.obj-title {
    font-size: 1.8rem;
}</style>