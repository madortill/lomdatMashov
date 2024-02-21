<template>
    <div id="feedback-call">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>

            <div v-if="indexInfo === 0">
               

            </div>

            <div v-if="indexInfo === 1" class="burger-container">
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
            arrayTitle: ['מבנה חלון גוהרי', 'מבנה שיחת המשוב', 'העלאת תופעות במשוב'],
            arrayInfo: ['עיקר שיחת המשוב היא התמקדות בחלק העיוור - מה שאנחנו מודעים אליו והנחנך לא.', 'לפי שיטת הסנדוויץ', 'איך עושים את זה?'],
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
    top:2vh;
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


</style>
