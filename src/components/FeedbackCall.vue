<template>
  <div id="feedback-call">
    <div class="div-text">
      <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
      <p class="info-text">{{ arrayInfo[indexInfo] }}</p>

      <div v-if="indexInfo === 0" class="flip-container">
        <div
          v-for="(item, index) in arrayAreaType"
          :key="index"
          :class="['flip-card-fc', this.onStart]"
        >
          <div
            class="flip-card-inner-fc"
            :style="`--hue: ${index * 18 + 215}deg`"
          >
            <div class="flip-card-front-fc">
              <h1 class="textBack">{{ arrayAreaType[index] }}</h1>
            </div>
            <div class="flip-card-back-fc">
              <h1 class="textBack">{{ arrayTextAreaType[index] }}</h1>
            </div>
          </div>
        </div>
      </div>
      <div v-if="indexInfo === 1" class="eye-container">
        <eyeGifSvg></eyeGifSvg>
      </div>

      <div v-if="indexInfo === 2" class="burger-container">
        <p class="text-feedBack1">{{ arrayFeedback[0] }}</p>
        <img
          src="@/assets/media/BP/arrow-left.png"
          alt="arrow-left"
          class="arrow-left-burger1"
        />
        <img
          v-for="(item, index) in burgerArray"
          :key="index"
          :src="src(item)"
          class="burger"
        />
        <p class="text-feedBack2">{{ arrayFeedback[1] }}</p>
        <img
          src="@/assets/media/BP/arrow-right.png"
          alt="arrow-right"
          class="arrow-right-burger"
        />
        <p class="text-feedBack3">{{ arrayFeedback[2] }}</p>
        <img
          src="@/assets/media/BP/arrow-left.png"
          alt="arrow-left"
          class="arrow-left-burger2"
        />

        <!-- <img src = "@/assets/media/burger/burgerEnd.svg" alt ="burgerEnd" class="burger"> -->
      </div>
      <div v-if="indexInfo === 3">
        <ul class="ul-right">
          <li
            v-for="(item, index) in correctArray"
            :key="index"
            class="list-text"
            :style="`--hue: ${index * 8 + 200}deg`"
          >
            {{ item }}
          </li>
        </ul>
      </div>
      <div v-if="indexInfo === 4" class="behavior-container">
        <!-- <p class="textBehave"> לחצו על ההתנהגות:</p> -->
        <div>
          <h1 @click="openlistP" class="title-behavior-p">
            {{ proveBehavior[0].typeTitle }}
          </h1>
          <Transition>
            <ul v-show="showListP" class="ulP">
              <li
                v-for="(item, index) in proveBehavior[0].arrayBehave"
                :key="index"
                class="list-text-p"
              >
                {{ item }}
              </li>
            </ul>
          </Transition>
        </div>
        <Transition>
          <img
            v-show="showBtnArrow"
            src="@/assets/media/FC/ion--arrow-undo-outline.svg"
            class="arrow-img"
          />
        </Transition>
        <div>
          <h1 @click="openlistS" class="title-behavior-s">
            {{ saveBehavior[0].typeTitle }}
          </h1>
          <Transition>
            <ul v-show="showListS" class="ulS">
              <li
                v-for="(item, index) in saveBehavior[0].arrayBehave"
                :key="index"
                class="list-text-s"
              >
                {{ item }}
              </li>
            </ul>
          </Transition>
        </div>
      </div>
      <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
      <button class="nextBtn" @click="nextBtn">המשך</button>
    </div>
  </div>
</template>

<script>
import eyeGifSvg from "./eyeGifSvg.vue";
import playGray from "@/assets/media/FC/playGray.png";
import playFull from "@/assets/media/FC/playFull.png";

export default {
  name: "feedback-call",
  components: {
    eyeGifSvg,
  },
  data() {
    return {
      imageSrc: [playGray, playFull],
      arrayFeedback: ["תופעה לשימור.", "העלאת  תופעה לשיפור.", "תופעה לשימור."],
      correctArray: [
        "יצירת חוזה",
        "מתן ביטוי לנחנך",
        "איסוף מידע חסר",
        "העלאת תופעה לשימור",
        "העלאת 2-3 תופעות לשיפור",
        "העלאת תופעה נוספת לשימור",
        "סיכום המשוב",
      ],
      imageSrc: playGray,
      onStart: "start",
      subj: 2,
      index: 0,
      arrayTitle: [
        "מבנה חלון גוהרי:",
        " שיחת המשוב.",
        "מבנה שיחת המשוב.",
        "מבנה העקרוני של שיחת משוב:",
        "העלאת תופעות במשוב.",
      ],
      arrayAreaType: [
        "איזור גלוי",
        "איזור עיוור",
        "איזור לא מודע",
        "איזור נסתר",
      ],
      arrayTextAreaType: [
        "ידוע לי וידוע לאחרים.",
        " ידוע לי ולא ידוע לאחרים.",
        "לא ידוע לי ולא ידוע לאחרים.",
        " לא ידוע לי וידוע לאחרים.",
      ],
      arrayInfo: [
        " חלון גוהרי הוא כלי להבנה ותרגול המתאר מודול איזורים לפי:",
        "עיקר שיחת המשוב היא התמקדות בחלק העיוור - מה שאנחנו מודעים אליו והנחנך לא.",
        "המשוב האפקטיבי יועבר בשיטת ה - סנדוויץ:",
        "",
        "איך עושים את זה?",
      ],
      proveBehavior: [
        {
          typeTitle: "התנהגות שלילית לשיפור",
          arrayBehave: [
            "העלאת תופעה אפשרית.",
            "ציון דוגמאות.",
            "איתור הסיבה האמיתית לתופעה.",
            "טיפול במקור התופעה.",
            "הצעת בנק פתרונות.",
            "בחירת הפיתרון המועדף.",
            "קביעת תוכנית ליישום הפיתרון.",
          ],
        },
      ],
      saveBehavior: [
        {
          typeTitle: "התנהגות חיובית לשימור",
          arrayBehave: [
            "העלאת תיאור ההתנהגות.",
            "ציון דוגמאות.",
            "איתור סיבת התופעה.",
            "הסבר על תרומת התנהגות.",
          ],
        },
      ],
      showBtnArrow: false,
      burgerArray: [
        "bunTop.svg",
        // 'lettuce.svg',
        // 'onion.svg',
        "patty.svg",
        // 'tomato.svg',
        "bunBottom.svg",
      ],
      indexTitle: 0,
      indexInfo: 0,
      showQ: true,
      showListP: false,
      showListS: false,
      clickBtnP: 0,
      clickBtnS: 0,
    };
  },
  mounted() {
    if (this.indexTitle === 0) {
      setTimeout(() => {
        this.onStart = "off";
      }, 100);
    }
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
        setTimeout(() => {
          this.showBtnArrow = true;
        }, 3000);
      }
      if (this.indexTitle === 5) {
        this.$emit("move-to-next", this.showQ);
      }
    },
    src(name) {
      return new URL(`../assets/media/burger/${name}`, import.meta.url).href;
    },
    openlistP() {
      if (this.clickBtnP % 2 === 0) {
        this.showListP = true;
        event.target.classList.add("borderRed");
      } else {
        this.showListP = false;
        event.target.classList.remove("borderRed");
      }
      this.clickBtnP++;
    },
    openlistS(event) {
      if (this.clickBtnS % 2 === 0) {
        this.showListS = true;
        event.target.classList.add("borderGreen");
      } else {
        this.showListS = false;
        event.target.classList.remove("borderGreen");
      }
      this.clickBtnS++;
    },
  },
};
</script>

<style>
.burger {
  width: 17%;
  transition: transform 0.3s ease;
  margin-bottom: 2%;
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
  /* cursor: pointer; */
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

.flip-card-fc:hover .flip-card-front-fc,
.flip-card-fc.start .flip-card-front-fc {
  transform: rotateY(180deg);
}

.flip-card-fc:hover .flip-card-back-fc,
.flip-card-fc.start .flip-card-back-fc {
  transform: rotateY(360deg);
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
  /* cursor: pointer; */
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
  /* cursor: pointer; */
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

.list-text-s,
.list-text-p {
  list-style: none;
  padding: 15px 30px;
  font-size: 1.4rem;
  transition: background-color 0.5s ease;
  color: rgb(52, 50, 50);
}

.list-text-s:hover,
.list-text-p:hover {
  /* cursor: pointer; */
  background-color: #dbdbdb;
  color: black;
}

.title-behavior-s {
  animation: floatAnimation 3s ease-in-out infinite;
  color: #57a84c;
  font-size: 2.4rem;
  margin: 15px;
  cursor: pointer;
  text-decoration: none;
  position: relative;

  &:hover {
    color: #57a84c;

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
    background-color: #57a84c;
    visibility: hidden;
    transform: scaleX(0);
    transition: all 0.3s ease-in-out 0s;
  }
  /* border: 1px solid rgb(42, 136, 35); */
}

.title-behavior-p {
  animation: floatAnimation 3s ease-in-out infinite;
  color: rgb(177, 28, 28);
  font-size: 2.4rem;
  margin: 15px;
  cursor: pointer;
  text-decoration: none;
  position: relative;

  &:hover {
    color: rgb(177, 28, 28);

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
    background-color: rgb(177, 28, 28);
    visibility: hidden;
    transform: scaleX(0);
    transition: all 0.3s ease-in-out 0s;
  }

  /* border-bottom: 1px solid rgb(177, 28, 28); */
}

.ulS,
.ulP {
  list-style: none;
  background-color: #fefefe;
  box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
  border-radius: 20px;
  overflow: hidden;
  padding: 0;
}

/* .borderGreen {
    border-bottom: 1.5px solid #57a84c;
}

.borderRed {
    border-bottom: 1.5px solid rgb(177, 28, 28);

} */

.textBehave {
  font-size: 1.5rem;
  position: absolute;
  top: 33%;
  color: #5f5a5a;
  position: fixed;
}

.arrow-left,
.arrow-right {
  position: absolute;
  width: 2%;
  animation: forwardArrow 2s ease-in-out infinite;
}

.arrow-left {
  right: 44%;
  top: 37%;
}

.arrow-right {
  left: 44%;
  top: 37%;
}

.list-text {
  font-size: 1.5rem;
  list-style: none;
  padding: 20px 35px;
  margin: 15px;
  transition: background-color 0.5s ease;
  background-color: hsl(var(--hue), 70%, 70%);
  border-radius: 15px;
  color: rgb(255, 255, 255);
}

.ul-right {
  position: absolute;
  top: 25%;
  left: 39%;
  padding: 0%;
}

@keyframes forwardArrow {
  0% {
    transform: translateX(0);
  }

  50% {
    transform: translateX(-10px);
  }

  100% {
    transform: translateX(0);
  }
}

.arrow-left-burger1,
.arrow-left-burger2,
.arrow-right-burger {
  position: absolute;
  width: 4%;
  animation: forwardArrow 2s ease-in-out infinite;
}

.arrow-left-burger1 {
  left: 35%;
  top: 39%;
}

.arrow-left-burger2 {
  top: 62%;
  left: 35%;
}

.arrow-right-burger {
  right: 34%;
  top: 50%;
}

.text-feedBack1,
.text-feedBack2,
.text-feedBack3 {
  position: absolute;
  font-size: 2rem;
  color: #db7c26;
  font-family: Heebo-Bold;
  animation: floatAnimation 3s ease-in-out infinite;
}

.text-feedBack1 {
  left: 20%;
  top: 37.5%;
}

.text-feedBack2 {
  right: 11%;
  top: 48%;
}

.text-feedBack3 {
  top: 60%;
  left: 20%;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.arrow-img {
  position: absolute;
  width: 5%;
  right: 11%;
  top: 33.7%;
  animation: forwardArrow 2s ease-in-out infinite;
}
</style>
