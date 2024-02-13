<template>
    <div id="basic-principles">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
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

.warpper {
    --cards: 4;
    --curvature: 72deg;
    counter-reset: cards;
    position: absolute;
    width: 100%;
    display: flex;
    justify-content: center;
    transform: translateY(420px);
    transform-style: preserve-3d;
    list-style: none;
}

.warpper>* {
    --curve: calc(var(--curvature) * ((var(--index) - (var(--cards) - 1) / 2) / var(--cards)));
    position: absolute;
    background-color: #010000;
    counter-increment: cards;
    flex: 0 0 auto;
    width: 20vw;
    max-width: 25vh;
    /* aspect-ratio:  2/3; */
    transform-origin: 50% 100%;
    transform: rotate(var(--curve)) translateY(-225%);
    transition: all 0.3s;
    cursor: pointer;
    font-size: 11vmin;
    transform-style: preserve-3d;
    border-radius: 4px;
}

.warpper>*:nth-child(1) {
    --index: 0;
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
.prevBtn:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
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

.tillburger {
    color: white;
    font-family: "Rubik";
    background-image: url("../../assets/images/tillburger/bg.svg");
    background-size: 100% 100%;
    background-repeat: no-repeat;
}

#tillburgerToppingsContainer,
.tillburgerToppingsFeedback {
    flex-basis: 0;
    -ms-flex-positive: 1;
    flex-grow: 1;
    display: flex;
    -ms-flex-direction: column;
    flex-direction: column;
    padding-left: 0;
    margin-bottom: 0;
    padding-right: 0;
    align-content: center;
    align-items: center;
    justify-content: space-between;
    height: 32vh;
    margin-bottom: 7vh;
}

.tillburgerTopping {
    position: relative;
    display: block;
    width: 75vw;
    height: 11vh;
    margin-bottom: -11vh;
    background-size: 100% 100%;
    background-repeat: no-repeat;
    display: flex;
    justify-content: center;
    align-items: flex-end;
}

.toppingText {
    text-align: center;
    height: 6vh;
    width: 60vw;
    display: flex;
    align-content: center;
    justify-content: center;
    align-items: center;
    padding-bottom: 0.2rem;
}

.lettuce {
    background-image: url("../../assets/images/tillburger/lettuce.svg");
}

.tomato {
    background-image: url("../../assets/images/tillburger/tomato.svg");
}

.patty {
    background-image: url("../../assets/images/tillburger/patty.svg");
}

.onion {
    background-image: url("../../assets/images/tillburger/onion.svg");
}

.buns {
    width: 75vw;
    background-size: 100% 100%;
    background-repeat: no-repeat;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.4rem;
    font-weight: 800;
}

.topBun {
    margin-bottom: -4vh;
    position: relative;
    z-index: 25;
    background-image: url("../../assets/images/tillburger/bunTop.svg");
    height: 14vh;
}

.bottomBun {
    background-image: url("../../assets/images/tillburger/bunBottom.svg");
    height: 9vh;
    padding-top: 0.5rem;
}

.tillburgerSubmitButton {
    width: 34vw;
    position: absolute;
    left: 4vw;
    bottom: 2vh;
}

#tillburgerExerInstruction {
    text-align: center;
    position: absolute;
    top: 10vh;
    font-size: 1.4rem;
    width: 100vw;
    height: 11vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 0.6rem;
    box-sizing: border-box;
}

#tillburgerLifeContainer {
    width: 100vw;
    position: absolute;
    top: 5vh;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 1.4rem;
}

.tillburgerLifeFries {
    width: 16vw;
    padding: 0.3rem;
}

.menu {
    background-image: url("../../assets/images/tillburger/menuBg.svg");
    background-size: 100% 100%;
    background-repeat: no-repeat;
    width: 91vw;
    height: 85vh;
}

.tillburgerFeedback {
    width: 91vw;
    text-align: center;
    font-size: 1.3rem;
    position: absolute;
    top: 2vh;
    padding: 1rem;
    box-sizing: border-box;
    height: 12vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

#tillburgerNextButton,
#tillburgerStartButton {
    position: absolute;
    bottom: 6vh;
    padding: 0.5rem 0.8rem;
    background-color: #aa6e2d;
    border-radius: 1.5rem;
}

.tillburgerEndImg {
    width: 71vw;
    top: 15vh;
}

.endTillburgerText {
    position: absolute;
    top: 51vh;
    text-align: center;
    padding: 0 2rem;
    font-size: 1.2rem;
}

.endTillburgerText2 {
    position: absolute;
    top: 61vh;
    text-align: center;
    padding: 0 2rem;
    width: 91vw;
    box-sizing: border-box;
    font-size: 1.2rem;
}

#tillburgerOpeningPage {
    z-index: 4;
}

#tilburgerStartText {
    width: 70vw;
    font-size: 1.3rem;
    line-height: 1.6;
    text-align: center;

}

#tillburgerStartHeadline {
    width: 91vw;
    text-align: center;
    font-size: 1.6rem;
    position: absolute;
    top: 8vh;
    padding: 1rem;
    box-sizing: border-box;
    font-weight: bold;
}</style>
