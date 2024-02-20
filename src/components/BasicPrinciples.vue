<template>
    <div id="basic-principles">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <button v-if = "showBtnCall" class = "callBtn" @click="nextBtn" >שיחת משוב</button>

        <!-- flipcards -->
        <div v-show = "indexTitle === 2" class="flip-card-container">
            <p class = "over-me">עברו מעליי!</p>
            <div v-for="( item, index) in arrayFront" :key="index" class="flip-card">
                <div class="flip-card-inner" :style="`--hue: ${index * 15 + 130}deg`">
                    <div class="flip-card-front">
                        <img :src="src(item)" class="imgFront">
                    </div>
                    <div class="flip-card-back">
                        <h1 class = "textBack">{{ arrayBack[index] }} </h1>
                    </div>
                </div>
            </div>
        </div>

        <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
        <button v-if = "!showBtnCall" class="nextBtn" @click="nextBtn">המשך</button>
    </div>
</template>

<script>

export default {
    name: 'basic-principles',
    components: {

    },
    data() {
        return {
            arrayFront: ['ear.svg', 'hands-heart.svg', 'auction.svg', 'headache.png', 'crossed-eye.svg'],
            arrayBack: ['פתיחות והקשבה', 'השריית אווירה נוחה, חיובית ובונה', 'חוסר שיפוטיות', 'לגיטימציה לטעויות ואי הסכמה', 'הבטחת סודיות'],
            arrayTitle: ["אז מהו משוב?", "המשוב האישי מתבסס על שני עקרונות על", "עקרונות היסוד של המשוב - תמיכה באגו", "עקרונות היסוד של המשוב - איסוף מקסימום מידע מהנחנך"],
            arrayInfo: ["משוב הוא מידע על התנהגות בעבר, אשר נמסר בהווה ועשוי להשפיע על ההתנהגות בעתיד.", '', '', 'בתור חונכים עלינו לאסוף מקסימום מיד מביצועי הנחנך. הנחנך תמיד מחזיק במידע ש-לך, כחונך, לא יהיה: שיקוליו, כיצד נראה הביצוע מנקודה מבטו, תחושותיו וחוויתו. אז מה עושים? '],
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
            
            if(this.indexTitle === 3) {
                this.showBtnCall = true;
            } else {
                this.showBtnCall = false;
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            if(this.indexTitle === 3) {
                this.showBtnCall = true;
            } else {
                this.showBtnCall = false;
            }
            if (this.indexTitle === 4) {
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
    position: absolute;
    width: 100%;
    height: 60%;
    top: 20%;
    text-align: center;
}

.info-text {
    padding: 2% 25%;
    font-size: 1.8rem;
    display: block;
}

.title-text {
    margin: auto;
    font-size: 2.5rem;
}

.nextBtn {
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
.callBtn:hover
 {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}

.callBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    border-radius: 100px;
    background-color: #055169;
    color: #ffffff;
    min-width: 15%;
    max-width: 10%;
    height: 10%;
    font-size: 2rem;
    left: 50%;
    transform: translateX(-50%); 
    top: 55%;
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
    left: 10%;
    height: 80%;
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
    background-color: #f0a06a;
    background-color: hsl(var(--hue), 50%, 58%);
    border-radius: 30px;
    color: black;
}

.flip-card-back {
    background-color: #f5c381;
    background-color: hsl(var(--hue), 50%, 78%);
    border-radius: 30px;
    color: rgb(84, 82, 82);
    transform: rotateY(180deg);
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
}

.imgFront {
    width: 60%;
    position: absolute;
    left: 20%;
    top:20%;
}

.over-me {
    position: absolute;
    top :25%;
    margin-left: 50%;
    font-size: 1.4rem;
    color: #5f5a5a;
    animation: floatAnimation 3s ease-in-out infinite;
}

.textBack {
    padding: 5%;
}
</style>
