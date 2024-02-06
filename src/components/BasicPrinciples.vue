<template>
    <div id="basic-principles">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <button v-if = "index > 0" class="prevBtn" @click="prevBtn">חזור</button>
        <button class="nextBtn" @click="nextBtn">המשך</button>
    </div>
</template>

<script>

export default {
    name: 'basic-principles',
    components: {

    },
    data() {
        return {
            showQ: false,
            index: 0,
            subj: 1,
            indexTitle: 0,
            indexInfo: 0,
            arrayTitle: ["מהו משוב?", "המשוב האישי מתבסס על שני עקרונות על", "עקרונות היסוד של המשוב - תמיכה באגו", "עקרונות היסוד של המשוב - איסוף מקסימום מידע מהנחנך"],
            arrayInfo: ["משוב הוא מידע על התנהגות בעבר, אשר נמסר בהווה ועשוי להשפיע על ההתנהגות בעתיד"],
        };
    },
    methods: {
        prevBtn() {
            if(this.index > 0) {
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
            if(this.indexTitle === 4) {
                this.$emit('move-to-next', this.showQ);
            }
        },
    },
}
</script>

<style>
.div-text {
    position: absolute;
    width: 50%;
    height: 50%;
    left: 25%;
    bottom: 25%;
    /* background-color: #a5c6e5; */
    border-radius: 10px;
    text-align: center;
}

.info-text {
    padding: 5%;
    margin: auto;
}

.title-text {
    padding: 5%;
    margin: auto;
}

.nextBtn {
    background-color: #006998;
    position: absolute;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    cursor: pointer;
    width: 9%;
    height: 6%;
    left: 10%;
    bottom: 13%;
    transition: background-color 0.3s linear;
}

.nextBtn:hover {
    background-color: #00A4E6;
}

.prevBtn {
    background-color: #006998;
    position: absolute;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    cursor: pointer;
    width: 9%;
    height: 6%;
    bottom: 13%;
    right: 10%;
    transition: background-color 0.3s linear;
}

.prevBtn:hover {
    background-color: #00A4E6;
}
</style>
