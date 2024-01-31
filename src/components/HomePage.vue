<template>
    <div id="home-page">
        <div v-if="showExplain">
            <div class="explain-page">
                <h2>הוראות ללומדה</h2>
                <p>כל מיני הסברים על הלומדה ועל השימוש בה</p>
            </div>
            <button id="expBtn" class="contBtn" @click="nextInfo"> המשך </button>
        </div>
        <div v-else>
            <div v-if = "!showQuestions">
                <navbar v-if = "showNav" :titleIndex="titleIndex"></navbar>
                <information-page  :titleIndex="titleIndex" @move-sub="moveSub" @close-nav = "closeNav" ></information-page>
            </div>
            <div v-if = "showQuestions"> 
                <quick-questions :indexQuestion = "indexQuestion" @next-sub = "nextSub"></quick-questions>
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
            titleIndex: 0,
            showNav: true,
            showQuestions: false,
            indexQuestion: 1,
        };
    },

    methods: {
        nextInfo(event) { // for explain btn
            this.showExplain = false;
        },
        nextSub() {
            this.showQuestions = false;
        },
        moveSub() {
            this.titleIndex++;
            if(this.titleIndex === 2) {
                this.showQuestions = true;
                this.indexQuestion = 0;
            } else if(this.titleIndex === 3) {
                this.showQuestions = true;
                this.indexQuestion = 2;
            } else if(this.titleIndex === 4) {
                this.showQuestions = true;
                this.indexQuestion = 3;
            }

            if (this.titleIndex === 4) {
                this.$emit('next-page');
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

.contBtn:hover {
    background-color: #00A4E6;
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
</style>
