<template>
    <div id="basic-principles">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <!-- what is mashov -->
        <div v-show="indexTitle === 0">
            <!-- <img src = "@/assets/media/BP/pfp.svg" class = "past-future-present-img"> -->
            <pfpSvg></pfpSvg>
            <img src = "@/assets/media/BP/future.svg" class = "future-text">
            <img src = "@/assets/media/BP/past.svg" class = "past-text">
            <img src="@/assets/media/BP/present.svg" class="present-text">
        </div>

        <!-- animation merge circle -->
        <div v-show="indexTitle === 1" class="principle-div">
            <div v-for="(item, index) in arrayPrinciple" :key="index" class="circle">
                {{ arrayPrinciple[index] }}
            </div>
            <button class="mergeBtn">מיזוג</button>
        </div>

        <!-- ago section -->
        <div v-show="indexTitle === 2" class="ago-container">
            <div v-for="(item, index) in arrayAgo" :key="index" class="circle-ago" :style="`--hue: ${index * 15 + 170}deg`">
                {{ arrayAgo[index] }}
            </div>
        </div>

        <!-- flipcards -->
        <div v-show="indexTitle === 3" class="flip-card-container">
            <div v-for="( item, index) in arrayFront" :key="index" class="flip-card">
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

        <div v-if="showBtnCall">
            <p class="text-btnCall">{{ arrayInfo[indexInfo + 1] }}</p>
            <button class="callBtn" @click="nextBtn">שיחת משוב</button>
        </div>
        <p v-if="indexTitle === 3 || indexTitle === 2" class="over-me">עברו מעליי!</p>
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

            arrayTitle: ["אז מהו משוב?", "המשוב האישי מתבסס על שני עקרונות על", "עקרונות היסוד של המשוב - תמיכה באגו", "עקרונות היסוד של המשוב - תמיכה באגו", "עקרונות היסוד של המשוב - איסוף מקסימום מידע מהנחנך"],
            arrayInfo: ["משוב הוא מידע על התנהגות בעבר, אשר נמסר בהווה ועשוי להשפיע על ההתנהגות בעתיד.", '', 'המשוב בעצם מהותו, נתפס כמאיים ביותר. הסיבות לכך הן:', 'על מנת לבטל את הגורמים המאיימים על אגו הנחנך, נקפיד על העקרונות הבאים:', 'בתור חונכים עלינו לאסוף מקסימום מיד מביצועי הנחנך. הנחנך תמיד מחזיק במידע ש-לך, כחונך, לא יהיה: שיקוליו, כיצד נראה הביצוע מנקודה מבטו, תחושותיו וחוויתו. ', 'אז מה עושים?'],
            arrayAgo: ['חוסר וודאות מצד הנחנך.', 'מעמד החונך.', 'דרישה לשינוי דפוסי התנהגות עמוקים.', 'ביקורת = כישלון.'],
            arrayPrinciple: ['תמיכה באגו הנחנך', 'איסוף מקסימום מידע מהנחנך'],
            showQ: false,
            index: 0,
            subj: 1,
            indexTitle: 0,
            indexInfo: 0,
            showBtnCall: false,

        };
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
        },
        src(name) {
            return new URL(`../assets/media/BP/${name}`, import.meta.url).href
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
    padding: 2% 30%;
    font-size: 1.8rem;
    display: block;
    z-index: 1;
    color: #3a3737;
}

.title-text {
    margin: auto;
    font-size: 2.5rem;
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
    left: 10%;
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
    right: 10%;
}

.nextBtn:hover,
.prevBtn:hover,
.callBtn:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}

.callBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    border-radius: 100px;
    background-color: #5998ab;
    color: #ffffff;
    min-width: 15%;
    max-width: 15%;
    height: 13%;
    font-size: 2rem;
    left: 50%;
    transform: translateX(-50%);
    top: 57%;
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

.flip-card:hover .flip-card-front {
    transform: rotateY(180deg);
}

.flip-card:hover .flip-card-back {
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
    cursor: pointer;
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
    cursor: pointer;
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
    font-size: 1.4rem;
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
    color: #5f5a5a;
    top: 45%;
}

.principle-div {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.circle {
    width: 15rem;
    height: 5rem;
    /* border-radius: 50%; */
    border-radius: 30PX;

    background-color: #7db9a5;
    text-align: center;
    color: #ffffff;
    font-size: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 2%;
    transition: all 0.3s ease;
    position: fixed;
    /* animation: floatAnimation 3s ease-in-out infinite; */
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
    cursor: pointer;
}

.mergeBtn {
    border: none;
    cursor: pointer;
    height: 5%;
    font-size: 1.6rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #3f7261;
    min-width: 10%;
    max-width: 15%;
}

.mergeBtn:hover {
    animation: hoverShine 200ms;
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
    padding: 2%;
    transition: all 0.3s ease;
    animation: floatAnimation 3s ease-in-out infinite;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
    background-color: hsl(var(--hue), 50%, 68%);
    position: fixed;
    padding: 2%;

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
    width:11%;
    top:47%;
    left: 51%;
    z-index: 0;
}
.past-text {
    position: absolute;
    width:11%;
    z-index: 0;
    top:62.5%;
    left: 39%;
}
.present-text {
    position: absolute;
    width:10%;
    top:81%;
    left: 51%;
    z-index: 0;
}
</style>
