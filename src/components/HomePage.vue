<template>
    <div id="home-page">
        <div v-if="showExplain">
            <div class="explain-page">
                <!-- <h1 style="font-size: 3rem;">הוראות ללומדה</h1> -->
                <p class = "explain-text">{{ explainArray[0] }} </p>
                <p class = "talk-text">שיחת משוב </p>
                <p class ="explain-text"> {{ explainArray[1] }}</p>
                <p  style="font-size: 2.3rem; color: #4b7189;"> בהצלחה!</p>
                <button id="expBtn" class="startBtn" @click="nextInfo"> התחל </button>
            </div>
        </div>
        <div v-if = "showGoal" class="finale-exe">
            <p v-for="(text, index) in array1" :key="text"
            :class="{ 'talk-text': index === 0 || index === 2, 'info-text-goal': index !== 0 && index !== 2 }"
            :style="{ 'font-size': index === 0 || index === 2 ? '3rem' : '1.6rem'}" >
                {{ text }} </p>
            <button id="expBtn" class="startBtn goalBtn" @click="nextToInfo"> המשך </button>
        </div>
        <div v-if = "showInformation">
            <div v-if="!showQuestions">
                <navbar v-if="showNav" :titleIndex="titleIndex"></navbar>
                <information-page :titleIndex="titleIndex" @move-sub="moveSub" @close-nav="closeNav"></information-page>
            </div>
            <div v-if="showQuestions">
                <quick-questions :indexQuestion="indexQuestion" @next-sub="nextSub"></quick-questions>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import InformationPage from '@/components/InformationPage.vue';
import QuickQuestions from '@/components/QuickQuestions.vue';

export default {
    name: 'home-page',
    components: {
        Navbar,
        InformationPage,
        QuickQuestions,
    },

    data() {
        return {
            showInfo: true,
            index: 0,
            showGoal: false,
            showExplain: true,
            titleIndex:  0,
            showNav: true,
            showQuestions: false,
            showInformation: false,
            indexQuestion: 0,
            array1: [
                'מטרת על',
                'החניך יעביר משוב אישי בצורה אפקטיבית.',
                'מטרות ביניים',
                'החניך יפרט עקרונות יסוד בשלב המשוב.',
                ' החניך יפרט את הכללים והמבנה הנכון של שיחת המשוב. ',
                'החניך יסביר את תהליך איתור מקורות אפשריים לתופעות במשוב.',
                'החניך יפרט את תהליך התמודדות עם התנגדויות במשוב.'
            ],
            explainArray: ['הינכם עומדים ללמוד, כיצד לנהל באופן המיטבי ביותר :', 'הלומדה אטרקטיבית ועניינית לכן תמצו ממנה את המיטב ועל הדרך נסו למצוא את דרכי הלימוד האטרקטיביות בלומדה.'],
        };
    },

    methods: {
        nextInfo(event) { // for explain btn
            this.showExplain = false;
            this.showGoal = true;
        },
        nextToInfo() {
            this.showGoal = false;
            this.showInformation = true;
        },
        nextSub() {
            this.showQuestions = false;
            console.log(this.titleIndex);
            if (this.titleIndex === 4) {
                this.$emit('next-page');
            }
        },
        moveSub(showQ) {
            console.log(showQ);
            this.showQuestions = false;

            if (showQ === true) {
                this.showQuestions = true;
                this.indexQuestion++;
            } else {
                this.showQuestions = false;
            }

            if (this.titleIndex >= 0 && this.titleIndex <= 4) {
                this.titleIndex++;
            }
        },
        closeNav() {
            this.showNav = false;
        }
    },
}
</script>

<style>
#home-page {
    background-color: #F2F2F2;
    width: 100%;
    height: 100vh;
    display: flex;
    position: relative;
    justify-content: center;
}

.startBtn {
    border: none;
    cursor: pointer;
    width: 25%;
    height: 7%;
    color:#ffffff;
    background-color: rgb(33, 116, 157);
    font-size: 1.6rem;
    border-radius: 100px;
    min-width: 12%;
}
.startBtn {
	animation: borderPulse 4000ms infinite ease-out;
}

.startBtn:hover,
.startBtn:focus {
	animation: borderPulse 4000ms infinite ease-out,  hoverShine 200ms;
}
@keyframes borderPulse {
  0% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255,.4), 0px 0px 0px 0px rgba(255,255,255,1);
  }
  35% {
    box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255,.2), 0px 0px 0px 10px rgba(255,255,255,0);
  }
  50% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255,.4), 0px 0px 0px 0px rgba(255,255,255,1);
  } 
  75% {
    box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255,.2), 0px 0px 0px 10px rgba(255,255,255,0);
  }
  100% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255,.4), 0px 0px 0px 0px rgba(255,255,255,1);
  }
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
/* Declare border pulse animation */

.explain-page {
    position: absolute;
    width: 40%;
    height: 70%;
    left: 30%;
    bottom: 20%;
    background: #fff;
    border-radius: 3rem;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
   
}

.explain-text {
    font-size: 2.1rem;
    padding: 1.5% 7% 2%;
    color: rgb(79, 77, 77);
    margin: 0%;
}

.goalBtn {
    position: absolute;
    bottom: 5%;
    left: 5%;
}
.info-text-goal {
    background-color: none;
    border-radius: 30px;
    height: 6%;
    transition: background-color 0.3s ease;
}
.info-text-goal:hover {
    background-color:#dbdbdb;
}
.talk-text {
    margin: 3%;
    animation: floatAnimation 3s ease-in-out infinite;
    color: #4b7189;
    font-size: 3rem;
    border-radius: 10px;
    top:1.5%;
    text-decoration: none;
    position: relative;
    cursor: default;
    &:hover {
        color: #4b7189;

        &:before {
            visibility: visible;
            transform: scaleX(1);
        }
    }

    &:before {
        content: "";
        position: absolute;
        width: 40%;
        height: 2px;
        bottom: 0;
        right: 30%;
        background-color: #4b7189;
        visibility: hidden;
        transform: scaleX(0);
        transition: all 0.3s ease-in-out 0s;
    }
}
</style>
