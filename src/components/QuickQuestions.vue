<template>
    <div id="quick-questions">
        <h1 class="title-question">{{ questions1[indexQ].title }}</h1>
        <div class="answers-container" @click="checkAnswer">
            <div class="row">
                <button id="1" ref="1"  class="pulse-button-hover">{{ questions1[indexQ].ans1 }}</button>
                <button id="2" ref="2" class="pulse-button-hover">{{ questions1[indexQ].ans2 }}</button>
            </div>
            <div class="row">
                <button id="3" ref="3" class="pulse-button-hover">{{ questions1[indexQ].ans3 }}</button>
                <button id="4" ref="4" class="pulse-button-hover">{{ questions1[indexQ].ans4 }}</button>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'quick-questions',
    props: ['indexQuestion'],
    components: {

    },
    data() {
        return {
            indexQ: 0,
            showAnswer: -1,
            wrongAnswer: 0,
            questions1: [
                {
                    title: "לפי מודל חלון גוהרי, באיזה אחד מהחלקים שיחת המשוב תתמקד?",
                    ans1: "בחלון הגלוי",
                    ans2: "בחלון העיוור",
                    ans3: "תבחלון הנסתר",
                    ans4: "בחלון הלא מודע",
                    correctAnswer: 2,
                },
                {
                    title: "לפי שיטת הסנדוויץ, מה המבנה העקרוני של שיחת המשוב?",
                    ans1: "תשובה 1",
                    ans2: "תשובה 2",
                    ans3: "תשובה 3",
                    ans4: "תשובה 4",
                    correctAnswer: 2,
                }, {
                    title: "מנה\י 4 כללים שעליהם נותן המשוב חייב להקפיד.",
                    ans1: "תשובה 1",
                    ans2: "תשובה 2",
                    ans3: "תשובה 3",
                    ans4: "תשובה 4",
                    correctAnswer: 1,
                },
            ],
            questions2: [
                {
                    title: "מפקד אשר מאמין כי שמירה על קשר עין חשובה יותר מהגעה לשיעור עם בקיאות מלאה בתוכן, ככל הנראה קיימת אצלו בעיה בטמונה באיזה מוקד?",
                    ans1: "תפיסה",
                    ans2: "מודעות",
                    ans3: "יישום",
                    ans4: "למידה",
                    correctAnswer: 1,
                }, {
                    title: "מנה\י 3 שאלות אפשריות למוקד המודעות.",
                    ans1: "תשובה 1",
                    ans2: "תשובה 2",
                    ans3: "תשובה 3",
                    ans4: "תשובה 4",
                    correctAnswer: 1,
                },
            ],
            questions3: [
                {
                    title: "במהלך משוב שמת לב כי המפקד שמולך נמרח על הכיסא ולא מרוכז. כיצד תמשיך\י את שיחת המשוב?",
                    ans1: "עצירה ושיקוף",
                    ans2: "שאילת שאלות",
                    ans3: "להמשיך כרגיל",
                    ans4: "תדווח למפקד שלו",
                    correctAnswer: 1,
                }, {
                    title: "נחנך שבשיחת המשוב החל לזרוק לעברך ביטויים עוקצניים ומזלזלים, נחשב לאיזה סוג של מתנגד?",
                    ans1: "הווכחן",
                    ans2: "הטראגי",
                    ans3: "היהיר",
                    ans4: "המסכים לכאורה",
                    correctAnswer: 3,
                }, {
                    title: "במידה ובמהלך התמודדות עם התנגדויות שיקפת ושאלת שאלות כלליות והתנהגות הנחנך לא השתנתה, כיצד תמשיך\י את ההתמודדות?",
                    ans1: "עצירת המשוב",
                    ans2: "שאילת שאלות ספציפיות",
                    ans3: "שיקוף",
                    ans4: "ויכוח עם הנחנך",
                    correctAnswer: 1,
                },
            ]
        };
    },
    methods: {
        checkAnswer(event) {
            if (event.target.classList.contains('pulse-button-hover')) {
                if (String(event.target.id) === String(this.questions1[this.indexQ].correctAnswer)) {
                    event.target.classList.add("correct");
                    // console.log('setTimeout');
                    if (this.indexQ < this.questions1.length - 1) {
                        setTimeout(() => {
                            for (let i = 1; i <= 4; i++) {
                                if (this.$refs[i].classList.contains('correct')) {
                                    this.$refs[i].classList.remove('correct');
                                }
                                if (this.$refs[i].classList.contains('wrong')) {
                                    this.$refs[i].classList.remove('wrong');
                                }
                            }
                            this.indexQ++;
                        }, 1500);
                    }
                    else if (this.indexQ === this.questions1.length - 1) {
                    setTimeout(() => {
                        this.$emit('next-sub');
                    }, 1500);
                }
                } else {
                    event.target.classList.add("wrong");
                }
            }
        },
    },
}
</script>

<style>
#quick-questions {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* height: 80vh;  */
}

.title-question {
    margin-bottom: 10%;
    color: #5f5a5a;
    padding: 10%;
    text-align: center;
    margin: 0;
}

.answers-container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.row {
    display: flex;
    margin-bottom: 10%;
}

.pulse-button-hover {
    background-color: #0492bd;
    margin: 0 2rem;
    cursor: pointer;
    border: none;
    font-size: 1.5rem;
    /* Adjust the font-size to make the buttons bigger */
    color: #ffffff;
    border-radius: 100px;
    padding: 10px 20px;

}

.pulse-button-hover:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}

/* .pulse-button-hover:focus  */


/* Declare border pulse animation */
@keyframes borderPulse {
    0% {
        box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255, 0.4), 0px 0px 0px 0px rgba(255, 255, 255, 1);
    }

    100% {
        box-shadow: inset 0px 0px 0px 3px rgba(24, 24, 176, 0.2), 0px 0px 0px 10px rgba(255, 255, 255, 0);
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

.correct {
    background-color: green;
}

.wrong {
    background-color: rgb(176, 6, 6);
}
</style>
