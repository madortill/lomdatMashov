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
    position: absolute;
    border: none;
    cursor: pointer;   
    height: 5%;
	font-size: 1.6rem;
	color: #ffffff;
	border-radius: 100px;
    background-color: #0492bd;
    min-width:10%;
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
    min-width:10%;
    max-width: 15%;
    bottom: 13%;
    right: 10%;
}

.nextBtn:hover,
.prevBtn:hover{
	animation: borderPulse 1000ms infinite ease-out,  hoverShine 200ms;
}


@keyframes hoverShine {
	0%{
		background-image: linear-gradient(135deg, rgba(255,255,255,.4) 0%, rgba(255,255,255,0) 50%, rgba(255,255,255,0) 100%);
	}
	50%{
		background-image: linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(255,255,255,.4) 50%, rgba(255,255,255,0) 100%);
	}
	100%{
		background-image: linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0) 50%, rgba(255,255,255,.4) 100%);
	}
}
</style>
