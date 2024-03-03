<template>
    <div id="home-page">
        <div v-if="showExplain">
            <div class="explain-page">
                <h1 style="font-size: 3rem;">הוראות ללומדה</h1>
                <p class = "explain-text">{{ explainArray[0] }} </p>
                <p class = "talk-text">שיחת משוב </p>
                <p class ="explain-text"> {{ explainArray[1] }}</p>
                <p  style="font-size: 2.3rem; color: #4b7189;"> בהצלחה!</p>
            </div>
            <button id="expBtn" class="contBtn" @click="nextInfo"> התחל </button>
        </div>
        <div v-else>
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
            showExplain: true,
            titleIndex: 3,
            showNav: true,
            showQuestions: false,
            indexQuestion: 0,
            explainArray: ['הינכם עומדים לעבור לומדה על כיצד לנהל באופן המיטבי ביותר :', 'הלומדה אטרקטיבית ועניינית לכן תמצו ממנה את המיטב ועל הדרך נסו למצוא את דרכי הלימוד האטרקטיביות בלומדה.'],
        };
    },

    methods: {
        nextInfo(event) { // for explain btn
            this.showExplain = false;
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

.contBtn {
    position: absolute;
    border: none;
    cursor: pointer;
    /* width: 12%; */
    height: 6%;
    left: 10%;
    bottom: 13%;
    font-size: 1.6rem;
    color: #ffffff;
    border-radius: 100px;
    background-color: #0492bd;
    min-width: 12%;
    max-width: 20%;
    left: 10%;
    bottom: 13%;
}

.contBtn {
    animation: borderPulse 1000ms infinite ease-out;
}

.contBtn:hover,
.contBtn:focus {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}


/* Declare border pulse animation */
@keyframes borderPulse {
    0% {
        box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, .4), 0px 0px 0px 0px rgba(255, 255, 255, 1);
    }

    100% {
        box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255, .2), 0px 0px 0px 10px rgba(255, 255, 255, 0);
    }
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
    font-size: 2rem;
    padding: 0% 10% 2%;
    color: rgb(79, 77, 77);
}


.talk-text {
    animation: floatAnimation 3s ease-in-out infinite;
    color: #f06543;
    font-size: 3rem;
    /* background-color: rgb(42, 136, 35); */
    border-radius: 10px;
    padding: 10px 30px;
    margin: 5px;

    cursor: pointer;
    text-decoration: none;
    position: relative;

    &:hover {
        color: #f26419;

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
        background-color: #f26419;
        visibility: hidden;
        transform: scaleX(0);
        transition: all 0.3s ease-in-out 0s;
    }
}
</style>
