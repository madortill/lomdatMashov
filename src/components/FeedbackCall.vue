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
            <div v-if="indexInfo === 1">
                <!-- ete animaion -->
                <!-- <img src = "@/assets/FC/gif.gif"> -->
            </div>
            <div v-if="indexInfo === 2" class="burger-container">
                <img v-for="( item, index) in burgerArray" :key="index" :src="src(item)" class="burger">
            </div>


            <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
            <button class="nextBtn" @click="nextBtn">המשך</button>
        </div>
    </div>
</template>

<script>

export default {
    name: 'feedback-call',
    components: {

    },
    data() {
        return {
            subj: 2,
            index: 0,
            arrayTitle: ['מבנה חלון גוהרי',' שיחת המשוב', 'מבנה שיחת המשוב', 'העלאת תופעות במשוב'],
            arrayAreaType: ['איזור פתוח', 'איזור עיוור', 'איזור לא ידוע', 'איזור חבוי'],
            arrayTextAreaType: ['ידוע לי וידוע לאחרים', 'לא ידוע לי וידוע לאחרים', 'לא ידוע לי ולא ידוע לאחרים', 'ידוע לי ולא ידוע לאחרים'],
            arrayInfo: [' חלון גוהרי הוא כלי להבנה ותרגול המתאר מודול איזורים לפי:', 'עיקר שיחת המשוב היא התמקדות בחלק העיוור - מה שאנחנו מודעים אליו והנחנך לא.', 'לפי שיטת הסנדוויץ', 'איך עושים את זה?'],
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
            if (this.indexTitle === 3) {
                this.$emit('move-to-next', this.showQ);
            }
        },
        src(name) {
            return new URL(`../assets/media/burger/${name}`, import.meta.url).href;
        },
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
    left: 50%; /* Adjust as needed */
    transform: translateX(-50%); 
}

.flip-card-fc {
    background-color: transparent;
    width: 200px;
    height: 200px;
    perspective: 1000px;
    margin: 10px;
    flex: 0 0 calc(50% - 20px); /* Each card takes 50% width with margin */
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

</style>
