<template>
    <div id="feedback-call">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>

            <div v-if="indexInfo === 0" class="flip-container">
                <div v-for="( item, index) in arrayAreaType" :key="index" class="flip-card-fc">
                    <div class="flip-card-inner-fc" :style="`--hue: ${index * 18 + 215}deg`">
                        <div class="flip-card-front-fc">
                            <h1 class="textBack">{{ arrayAreaType[index] }} </h1>
                        </div>
                        <div class="flip-card-back-fc">
                            <h1 class="textBack">{{ arrayTextAreaType[index] }} </h1>
                        </div>
                    </div>
                </div>

            </div>
            <div v-if="indexInfo === 1" class="eye-container">
                <eyeGifSvg></eyeGifSvg>
            </div>

            <div v-if="indexInfo === 2" class="burger-container">
                <img v-for="( item, index) in burgerArray" :key="index" :src="src(item)" class="burger">
            </div>

            <div v-if="indexInfo === 3" class="behavior-container">
                <div>
                    <!-- <img src ="@/assets/media/FC/playGray.png"  class = "playBtn pBtn"> -->
                    <img :src="imageSrc" alt="Image" @mouseover="changeImage('new-image.jpg')"
                        @mouseout="changeImage('original-image.jpg')" class="playBtn pBtn">
                    <h1 class="title-behavior-p">{{ behaviors[0].typeTitle }}</h1>
                    <ul v-show="showListP">
                        <li v-for="(item, index) in behaviors[0].arrayBehave" :key="index" class="list-text-p">
                            {{ item }}
                        </li>
                    </ul>
                </div>
                <div>
                    <!-- <img src ="@/assets/media/FC/playGray.png" class = "playBtn sBtn"> -->
                    <img :src="imageSrc" alt="Image" @mouseover="changeImage('new-image.jpg')"
                        @mouseout="changeImage('original-image.jpg')" class="playBtn sBtn">
                    <h1 class="title-behavior-s">{{ behaviors[1].typeTitle }}</h1>
                    <ul v-show="showListS">
                        <li v-for="(item, index) in behaviors[1].arrayBehave" :key="index" class="list-text-s">
                            {{ item }}
                        </li>
                    </ul>
                </div>
            </div>

            <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
            <button class="nextBtn" @click="nextBtn">המשך</button>
        </div>
    </div>
</template>

<script>
import eyeGifSvg from './eyeGifSvg.vue'

export default {
    name: 'feedback-call',
    components: {
        eyeGifSvg
    },
    data() {
        return {
            imageSrc: [
                '@/assets/media/FC/playGray.png',
                '@/assets/media/FC/playFull.png'
            ],
            subj: 2,
            index: 0,
            arrayTitle: ['מבנה חלון גוהרי', ' שיחת המשוב', 'מבנה שיחת המשוב', 'העלאת תופעות במשוב'],
            arrayAreaType: ['איזור פתוח', 'איזור עיוור', 'איזור לא ידוע', 'איזור חבוי'],
            arrayTextAreaType: ['ידוע לי וידוע לאחרים', 'לא ידוע לי וידוע לאחרים', 'לא ידוע לי ולא ידוע לאחרים', 'ידוע לי ולא ידוע לאחרים'],
            arrayInfo: [' חלון גוהרי הוא כלי להבנה ותרגול המתאר מודול איזורים לפי:', 'עיקר שיחת המשוב היא התמקדות בחלק העיוור - מה שאנחנו מודעים אליו והנחנך לא.', 'לפי שיטת הסנדוויץ', 'איך עושים את זה?'],
            behaviors: [
                {
                    type: 0,
                    typeTitle: 'התנהגות שלילית לשיפור',
                    arrayBehave: ['העלאת תופעה אפשרית', 'ציון דוגמאות', 'איתור הסיבה האמיתית לתופעה', 'טיפול במקור התופעה', 'הצעת בנק פתרונות', 'בחירת הפיתרון המועדף', 'קביעת תוכנית ליישום הפיתרון'],
                },
                {
                    type: 1,
                    typeTitle: 'התנהגות חיובית לשימור',
                    arrayBehave: ['העלאת תיאור ההתנהגות', 'ציון דוגמאות', 'איתור סיבת התופעה', 'הסבר על תרומת התנהגות'],
                },
            ],
            burgerArray: [
                'bunTop.svg',
                'lettuce.svg',
                'patty.svg',
                'onion.svg',
                'tomato.svg',
                'bunBottom.svg'
            ],
            indexTitle: 0,
            indexInfo: 0,
            showQ: true,
            showListP: true,
            showListS: true,
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
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            if (this.indexTitle === 4) {
                this.$emit('move-to-next', this.showQ);
            }
        },
        src(name) {
            return new URL(`../assets/media/burger/${name}`, import.meta.url).href;
        },
        openlistP() {
            this.showListP = true;
            this.showListS = true;

        },
        changeImage(newSrc) {
            this.imageSrc = newSrc;
        }
    },
}
</script>

<style>
.burger {
    width: 15%;
    transition: transform 0.3s ease;
    margin-bottom: 0.5%;
    /* position: relative; */
    top: 2vh;
}

.burger-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    /* height: 100%; */
    padding-top: 20px;
}

.burger:hover {
    cursor: pointer;
    transform: translateY(-20px);
}

.flip-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    position: absolute;
    left: 50%;
    /* Adjust as needed */
    transform: translateX(-50%);
}

.flip-card-fc {
    background-color: transparent;
    width: 170px;
    height: 220px;
    perspective: 1000px;
    margin: 10px;
    flex: 0 0 calc(50% - 20px);
    /* Each card takes 50% width with margin */
    box-sizing: border-box;
}

.flip-card-inner-fc {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
}

.flip-card-fc:hover .flip-card-front-fc {
    transform: rotateY(180deg);
}

.flip-card-fc:hover .flip-card-back-fc {
    transform: rotateY(360deg)
}

.flip-card-front-fc,
.flip-card-back-fc {
    transition: transform 0.6s;
    transform-style: preserve-3d;
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

.flip-card-front-fc {
    background-color: hsl(var(--hue), 50%, 58%);
    border-radius: 30px;
    color: rgb(254, 251, 251);
    font-size: 1.7rem;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.flip-card-back-fc {
    background-color: hsl(var(--hue), 50%, 80%);
    border-radius: 30px;
    color: rgb(37, 33, 33);
    font-size: 1.3rem;
    transform: rotateY(180deg);
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}

.eye-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 50vh;
}

.behavior-container {
    display: flex;
    justify-content: space-evenly;
}

.list-text-p {
    list-style: none;
    padding: 10px 30px;
    margin: 10px;
    font-size: 1.2rem;
    position: relative;
    background: #d55959;
    border-radius: 10px;
    color: whitesmoke;

}

.list-text-p:hover {
    cursor: pointer;
    text-decoration: none;

    &:hover {
        color: #b30000;

        &:before {
            visibility: visible;
            transform: scaleX(1);
        }
    }

    &:before {
        content: "";
        position: absolute;
        width: 100%;
        height: 3px;
        bottom: 0;
        left: 0;
        background-color: #b30000;
        visibility: hidden;
        transform: scaleX(0);
        transition: all 0.3s ease-in-out 0s;
    }
}

.list-text-s {
    list-style: none;
    padding: 10px 30px;
    margin: 10px;
    font-size: 1.2rem;
    position: relative;
    background: #41ab73;
    border-radius: 10px;
    color: whitesmoke;
}

.list-text-s:hover {
    cursor: pointer;
    position: relative;
    text-decoration: none;

    &:hover {
        color: #cfe7be;

        &:before {
            visibility: visible;
            transform: scaleX(1);
        }
    }

    &:before {
        content: "";
        position: absolute;
        width: 100%;
        height: 3px;
        bottom: 0;
        left: 0;
        background-color: #638f41;
        visibility: hidden;
        transform: scaleX(0);
        transition: all 0.3s ease-in-out 0s;
    }
}

.title-behavior-s {
    color: rgb(42, 136, 35);
    border-bottom: 1px solid rgb(42, 136, 35);
}

.title-behavior-p {
    color: rgb(177, 28, 28);
    border-bottom: 1px solid rgb(177, 28, 28);
}

.playBtn {
    position: absolute;
    width: 2%;
}

.playBtn:hover {
    cursor: pointer;
    /* background-image: url("@/assets/media/FC/playFull"); */
}

.sBtn {
    bottom: 58.5%;
    left: 38.5%;
}

.pBtn {
    left: 78.5%;
    bottom: 58.5%;
}</style>
