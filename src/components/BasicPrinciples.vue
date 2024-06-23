<template>
    <div id="basic-principles">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p :class="indexTitle === 4 ? 'info-div-text' : 'info-text'"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <!-- what is mashov -->
        <div v-show="indexTitle === 0">
            <pfpSvg></pfpSvg>
            <!-- <p class="over-me-text">עברו מעליי!</p> -->
            <img src="@/assets/media/BP/future.svg" class="future-text">
            <img src="@/assets/media/BP/past.svg" class="past-text">
            <img src="@/assets/media/BP/present.svg" class="present-text">
        </div>

        <!-- animation merge circle -->
        <div v-show="indexTitle === 1" class="principle-div">
            <div v-for="(item, index) in arrayPrinciple" :key="index" class="circle">
                {{ arrayPrinciple[index] }}
            </div>
            <img src="@/assets/media/BP/plus.png" alt="plus" class="plus-img">
            <p class="over-me-text">לחצו עליי</p>
            <button class="mergeBtn" @click="openMashov">מיזוג</button>
            <img src="@/assets/media/BP/equals.png" alt="equals" class="equals-img">
            <Transition>
                <p v-show="showMashov" class="mashov-div">משוב</p>
            </Transition>
        </div>

        <!-- ago section -->
        <div v-show="indexTitle === 2" class="ago-container">
            <div v-for="(item, index) in arrayAgo" :key="index" class="circle-ago" :style="`--hue: ${index * 15 + 170}deg`">
                {{ arrayAgo[index] }}
            </div>
        </div>

        <!-- flipcards -->
        <div v-show="indexTitle === 3" class="flip-card-container">
            <div v-for="( item, index) in arrayFront" :key="index" :class="['flip-card', this.onStart]">
                <div class="flip-card-inner" :style="`--hue: ${index * 15 + 130}deg`">
                    <div class="flip-card-front">
                        <img :src="src(item)" class="imgFront">
                    </div>
                    <div class="flip-card-back">
                        <h1 class="textBack">{{ arrayBack[index] }} </h1>
                    </div>
                </div>
            </div>
        </div>

        <div v-show="indexTitle === 4" class="back-div">

        </div>

        <div v-if="showBtnCall">
            <p class="text-btnCall">{{ arrayInfo[indexInfo + 1] }}</p>
            <img src="@/assets/media/BP/arrow-down.png" alt="arrow-down" class="arrowImgDown">
            <button class="callBtn" @click="nextBtn"> שיחת משוב</button>
        </div>

        <!-- <p v-if="indexTitle === 3 || indexTitle === 2" class="over-me">עברו מעליי!</p> -->
        <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
        <button v-if="!showBtnCall" class="nextBtn" @click="nextBtn">המשך</button>
    </div>
</template>

<script>
import pfpSvg from './pfpSvg.vue'

export default {
    name: 'basic-principles',
    components: {
        pfpSvg
    },
    data() {
        return {
            arrayFront: ['ear.svg', 'hands-heart.svg', 'auction.svg', 'headache.png', 'crossed-eye.svg'],
            arrayBack: ['פתיחות והקשבה.', 'השריית אווירה נוחה, חיובית ובונה.', 'חוסר שיפוטיות.', 'לגיטימציה לטעויות ואי הסכמה.', 'הבטחת סודיות.'],
            arrayTitle: ["אז, מהו משוב?", "המשוב האישי מתבסס על שני עקרונות על:", "עקרונות היסוד של המשוב - תמיכה באגו.", "עקרונות היסוד של המשוב - תמיכה באגו.", "עקרונות היסוד של המשוב - איסוף מקסימום מידע מהנחנך."],
            arrayInfo: ["משוב, הוא מידע על התנהגות בעבר, אשר נמסר בהווה ועשוי להשפיע על ההתנהגות בעתיד.", '', 'המשוב בעצם מהותו, נתפס כמאיים ביותר. הסיבות לכך הן:', 'על מנת לבטל את הגורמים המאיימים על אגו הנחנך, נקפיד על העקרונות הבאים:', 'בתור חונכים עלינו לאסוף מקסימום מידע מביצועי הנחנך. הנחנך תמיד מחזיק במידע שאצלך כחונך לא יהיה: שיקוליו, כיצד נראה הביצוע מנקודה מבטו, תחושותיו וחוויתו. ', 'אז מה עושים?'],
            arrayAgo: ['חוסר וודאות מצד הנחנך.', 'מעמד החונך.', 'דרישה לשינוי דפוסי התנהגות עמוקים.', 'ביקורת = כישלון.'],
            arrayPrinciple: ['תמיכה באגו הנחנך.', 'איסוף מקסימום מידע מהנחנך.'],
            showQ: false,
            index: 0,
            subj: 1,
            indexTitle: 0,
            indexInfo: 0,
            showBtnCall: false,
            showMashov: false,
            onStart: 'start'
        };
    },
    mounted () {

    },
    methods: {
        prevBtn() {
            if (this.index > 0) {
                this.index--;
            }
            if (this.indexTitle > 0 && this.indexInfo) {
                this.indexTitle--;
                this.indexInfo--;
            }

            if (this.indexTitle === 4) {
                this.showBtnCall = true;
            } else {
                this.showBtnCall = false;
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            if (this.indexTitle === 4) {
                this.showBtnCall = true;
            } else {
                this.showBtnCall = false;
            }
            if (this.indexTitle === 5) {
                this.$emit('move-to-next', this.showQ);
            }

            if (this.indexTitle === 3) {
                setTimeout(() => {
                    this.onStart = 'off';
                }, 100);
            }
        },
        src(name) {
            return new URL(`../assets/media/BP/${name}`, import.meta.url).href
        },
        openMashov() {
            this.showMashov = true;
        }

    },
}
</script>

<style>
.div-text {
    width: 100%;
    height: 60%;
    /* top: 15%; */
    text-align: center;
}

.info-text {
    position: relative;
    padding: 0% 20% 0 35%;
    right: 8%;
    font-size: 1.9rem;
    display: block;
    z-index: 1;
    color: #3a3737;
}

.info-div-text {
    position: relative;
    padding: 0% 20% 0 35%;
    right: 8%;
    font-size: 2.2rem;
    display: block;
    z-index: 1;
    color: #ffffff;
    margin-top: 4.5%;
}

.title-text {
    margin: auto;
    font-size: 3rem;
    padding-top: 2%;
}

.nextBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    height: 5%;
    font-size: 1.4rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #0492bd;
    min-width: 10%;
    max-width: 15%;
    left: 7%;
    bottom: 13%;
}

.prevBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    height: 5%;
    font-size: 1.6rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #0492bd;
    min-width: 10%;
    max-width: 15%;
    bottom: 13%;
    right: 8%;
}

.nextBtn:hover,
.prevBtn:hover,
.callBtn:hover {
    animation: borderPulse 4000ms infinite ease-out, hoverShine 200ms;
}

.callBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    border-radius: 100px;
    background-color: #67c6c7;
    color: #ffffff;
    min-width: 15%;
    max-width: 15%;
    height: 13%;
    font-size: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    top: 70%;
}

@keyframes hoverShine {
    0% {
        background-image: linear-gradient(135deg, rgba(255, 255, 255, .4) 0%, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, 0) 100%);
    }

    50% {
        background-image: linear-gradient(135deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, .4) 50%, rgba(255, 255, 255, 0) 100%);
    }

    100% {
        background-image: linear-gradient(135deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 0) 50%, rgba(255, 255, 255, .4) 100%);
    }
}

.flip-card-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    position: absolute;
    left: 8%;
    height: 50%;
    bottom: 20%;
}

.flip-card {
    background-color: transparent;
    width: 300px;
    height: 300px;
    perspective: 1000px;
    margin: 10px;
}

.flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
}

.flip-card:hover .flip-card-front, .flip-card.start .flip-card-front{
    transform: rotateY(180deg);
}

.flip-card:hover .flip-card-back, .flip-card.start .flip-card-back{
    transform: rotateY(360deg)
}

.flip-card-front,
.flip-card-back {
    transition: transform 0.6s;
    transform-style: preserve-3d;
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

.flip-card-front {
    background-color: hsl(var(--hue), 50%, 58%);
    border-radius: 30px;
    color: black;
    /* cursor: pointer; */
}

.flip-card-back {
    background-color: hsl(var(--hue), 50%, 78%);
    border-radius: 30px;
    color: rgb(84, 82, 82);
    transform: rotateY(180deg);
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    /* cursor: pointer; */
}

.imgFront {
    width: 60%;
    position: absolute;
    left: 20%;
    top: 20%;
}

.over-me {
    position: absolute;
    top: 70%;
    right: 10%;
    font-size: 1.2rem;
    color: #5f5a5a;
    /* animation: floatAnimation 3s ease-in-out infinite; */
}

.textBack {
    padding: 5%;
}

.text-btnCall {
    position: absolute;
    font-size: 2rem;
    left: 45%;
    color: #4f4a4a;
    top: 52%;
}

.principle-div {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.circle {
    width: 18rem;
    height: 7rem;
    /* border-radius: 50%; */
    border-radius: 100px;
    background-color: #68d8d6;
    text-align: center;
    color: #ffffff;
    font-size: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 2%;
    transition: all 0.3s ease;
    position: fixed;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
}

.circle:nth-child(1) {
    top: 30%;
    left: 25%;
}

.circle:nth-child(2) {
    top: 30%;
    right: 25%;
}

.circle-ago:hover {
    box-shadow: 0 15px 9px rgba(0, 0, 0, 0.4);
    width: 17rem;
    height: 17rem;
    padding: 2%;
    /* cursor: pointer; */
}

.mergeBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    font-size: 1.6rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #536e7e;
    min-width: 10%;
    height: 7%;
    top: 48%;
}

.mergeBtn:hover {
    animation: hoverShine 200ms;
}

.mashov-div {
    width: 15rem;
    height: 7rem;
    border-radius: 100px;
    background-color: #f5853f;
    text-align: center;
    color: #ffffff;
    font-size: 3.5rem;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 2%;
    transition: all 0.3s ease;
    position: absolute;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
    top: 62%;
}

.circle-ago {
    width: 15rem;
    height: 15rem;
    border-radius: 50%;
    text-align: center;
    /* color: #ffffff; */
    color: rgb(65, 63, 63);
    font-size: 2rem;
    font-weight: 550;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1.6%;
    transition: all 0.3s ease;
    animation: floatAnimation 3s ease-in-out infinite;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
    background-color: hsl(var(--hue), 50%, 68%);
    position: fixed;
}

.ago-container {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    padding: 1rem;
}

.circle-ago:nth-child(1) {
    left: 10%;
    bottom: 30%;
}

.circle-ago:nth-child(2) {
    left: 30%;
    bottom: 30%;
}

.circle-ago:nth-child(3) {
    left: 50%;
    bottom: 30%;
}

.circle-ago:nth-child(4) {
    left: 70%;
    bottom: 30%;
}

.future-text {
    position: absolute;
    width: 11%;
    top: 47%;
    left: 51%;
    pointer-events: none
}

.past-text {
    position: absolute;
    width: 11%;
    top: 62.5%;
    left: 39%;
    pointer-events: none
}

.present-text {
    position: absolute;
    width: 10%;
    top: 81%;
    left: 51%;
    pointer-events: none
}

.over-me-text {
    position: absolute;
    font-size: 1.2rem;
    color: #978f8f;
    top: 54%;
    left: 40%;
    /* transform: rotate(348deg); */
    animation: floatAnimation 3s ease-in-out infinite;
}

@keyframes floatAnimation2 {

    0%,
    100% {
        transform: rotate(348deg);
        /* Start and end position of the rotation */
    }

    50% {
        transform: rotate(360deg);
        /* Middle position of the rotation */
    }
}

.back-div {
    position: absolute;
    width: 55%;
    height: 23%;
    background-color: #83bfd2;
    border-radius: 40px;
    top: 30%;
    left: 22.5%;
}

.arrowImgDown {
    position: absolute;
    left: 48.5%;
    top: 62%;
    width: 2.5%;
    animation: floatAnimation 1s ease-in-out infinite;
}

.plus-img {
    position: absolute;
    top: 35%;
    width: 2%;
}

.equals-img {
    width: 3%;
    position: absolute;
    bottom: 35%;
}

.v-enter-active,
.v-leave-active {
    transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}

.v-enter-active,
.v-leave-active {
    transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>
