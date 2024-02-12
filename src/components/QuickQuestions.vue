<template>
    <div id="quick-questions">
        <h1 class="title-question">{{ this[`questions${this.indexQuestion}`][indexQ].title }}</h1>
        <div v-if="this[`questions${this.indexQuestion}`][indexQ].Qtype === 0" class="answers-container"
            @click="checkAnswer">
            <div class="row">
                <button id="1" ref="1" class="pulse-button-hover">{{ this[`questions${this.indexQuestion}`][indexQ].ans1
                }}</button>
                <button id="2" ref="2" class="pulse-button-hover">{{ this[`questions${this.indexQuestion}`][indexQ].ans2
                }}</button>
            </div>
            <div class="row">
                <button id="3" ref="3" class="pulse-button-hover">{{ this[`questions${this.indexQuestion}`][indexQ].ans3
                }}</button>
                <button id="4" ref="4" class="pulse-button-hover">{{ this[`questions${this.indexQuestion}`][indexQ].ans4
                }}</button>
            </div>
        </div>

        <div v-if="this[`questions${this.indexQuestion}`][indexQ].Qtype === 1" class="draggable-container">
            <p class="text"> * גרור את התשובה לפי הסדר המתאים.</p>
            <div class="draggable-area" @drop="(e) => {
                e.preventDefault();
                drop(e);
                checkDraggable(e)
            }" @dragover="allowDrop" id='dragArea' @dragstart="onDragging">
            </div>

            <div class="word-warehouse" draggable="true" @dragstart="onDragging" @dragover="allowDrop" @drop="(e) => {
                e.preventDefault();
                drop(e);
                checkDrop(e)
            }">
                <ul>
                    <li v-for="(item, index) in this[`questions${this.indexQuestion}`][this.indexQ].ansArray" :key="index"
                        class="list-item" draggable="true" @dragstart="drag" :id="'listItem' + index">
                        {{ item }} </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import Draggable from 'vuedraggable';

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
            indexItem: 0,
            newArray: [],
            // questions: [this.questions1, this.questions2, this.questions3],
            questions1: [
                {
                    Qtype: 0,
                    title: "לפי מודל חלון גוהרי, באיזה אחד מהחלקים שיחת המשוב תתמקד?",
                    ans1: "בחלון הגלוי",
                    ans2: "בחלון העיוור",
                    ans3: "תבחלון הנסתר",
                    ans4: "בחלון הלא מודע",
                    correctAnswer: 2,
                },
                {
                    Qtype: 1,
                    title: "לפי שיטת הסנדוויץ, מה המבנה העקרוני של שיחת המשוב?",
                    ansArray: [
                        "העלאת 2-3 תופעות לשיפור",
                        "העלאת תופעה לשימור",
                        "מתן ביטוי לנחנך",
                        "יצירת חוזה",
                        "סיכום המשוב",
                        "איסוף מידע חסר",
                        "העלאת תופעה נוספת לשימור"
                    ],
                    rightAns: [
                        3,
                        2,
                        5,
                        1,
                        0,
                        6,
                        4
                    ],
                }, {
                    Qtype: 1,
                    title: "מנה\י 4 כללים שעליהם נותן המשוב חייב להקפיד.",
                    ansArray: [
                        "איתור סיבת התופעה",
                        "הסבר על תרומת ההתנהגות",
                        "העלאת תיאור ההתנהגות",
                        "ציון דוגמאות",

                    ],
                    rightAns: [
                        2,
                        3,
                        0,
                        1,
                    ]
                },
            ],
            questions2: [
                {
                    Qtype: 0,
                    title: "מפקד אשר מאמין כי שמירה על קשר עין חשובה יותר מהגעה לשיעור עם בקיאות מלאה בתוכן, ככל הנראה קיימת אצלו בעיה בטמונה באיזה מוקד?",
                    ans1: "תפיסה",
                    ans2: "מודעות",
                    ans3: "יישום",
                    ans4: "למידה",
                    correctAnswer: 1,
                }, {
                    Qtype: 1,
                    title: "מנה\י 3 שאלות אפשריות למוקד המודעות.",
                    ansArray: [
                        "תשובה 1",
                        "תשובה 2",
                        "תשובה 3",
                        "תשובה 4",
                    ],
                    rightAns: [
                        0,
                        1,
                        2,
                        3,
                    ]
                },
            ],
            questions3: [
                {
                    Qtype: 0,
                    title: "במהלך משוב שמת לב כי המפקד שמולך נמרח על הכיסא ולא מרוכז. כיצד תמשיך\י את שיחת המשוב?",
                    ans1: "עצירה ושיקוף",
                    ans2: "שאילת שאלות",
                    ans3: "להמשיך כרגיל",
                    ans4: "תדווח למפקד שלו",
                    correctAnswer: 1,
                }, {
                    Qtype: 0,
                    title: "נחנך שבשיחת המשוב החל לזרוק לעברך ביטויים עוקצניים ומזלזלים, נחשב לאיזה סוג של מתנגד?",
                    ans1: "הווכחן",
                    ans2: "הטראגי",
                    ans3: "היהיר",
                    ans4: "המסכים לכאורה",
                    correctAnswer: 3,
                }, {
                    Qtype: 0,
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
    // mounted() {
    // console.log('q number:', this.indexQuestion);
    // console.log(this[`questions${this.indexQuestion}`]);
    // },
    methods: {
        checkAnswer(event) {
            if (event.target.classList.contains('pulse-button-hover')) {
                if (String(event.target.id) === String(this[`questions${this.indexQuestion}`][this.indexQ].correctAnswer)) {
                    event.target.classList.add("correct");
                    if (this.indexQ < this[`questions${this.indexQuestion}`].length - 1) {
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
                    else if (this.indexQ === this[`questions${this.indexQuestion}`].length - 1) {
                        setTimeout(() => {
                            this.$emit('next-sub');
                        }, 1500);
                    }
                } else {
                    event.target.classList.add("wrong");
                }
            }
        },

        onDragging(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        },

        allowDrop(ev) {
            ev.preventDefault();
        },

        drag(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        },

        drop(ev) {
            ev.preventDefault();
            const data = ev.dataTransfer.getData("text");
            ev.target.appendChild(document.getElementById(data));
            // this.checkDraggable(data);
        },

        checkDraggable(ev) {
            const data = ev.dataTransfer.getData("text");
            let indexCorrectAns = 0;
            this.newArray.push(data);
            const rightAns = this[`questions${this.indexQuestion}`][this.indexQ].rightAns;
            if (!rightAns) {
                console.log("rightAns is not defined or empty");
                return;
            }
            for (let i = 0; i < rightAns.length && i < this.newArray.length; i++) {
                const newArrayElement = this.newArray[i];
                const rightAnsElement = rightAns[i];
                if (Number(newArrayElement.slice(8)) === rightAnsElement) {
                    console.log('Correct');
                    indexCorrectAns++;
                    document.getElementById(data).classList.add("correct");
                } else {
                    console.log('Wrong');
                    document.getElementById(data).classList.add("wrong");
                }
                console.log(indexCorrectAns);
                if (indexCorrectAns === rightAns.length) {
                    setTimeout(() => {
                        this.indexQ++;
                    }, 1500)
                }
            }
        },

        checkDrop(ev) {
            const data = ev.dataTransfer.getData("text");
            // console.log( this.newArray);
            for (let i = 0; i < this.newArray.length; i++) {
                if (this.newArray[i] === data) {
                    this.newArray = this.newArray.filter(item => item !== data);
                    if (document.getElementById(data).classList.contains('correct')) {
                        document.getElementById(data).classList.remove('correct');
                    }
                    if (document.getElementById(data).classList.contains('wrong')) {
                        document.getElementById(data).classList.remove('wrong');
                    }
                } 
            }
        }
    },
}
</script>

<style>
#quick-questions {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* height: 60vh;  */
}

.title-question {
    /* margin-bottom: 5%; */
    color: #5f5a5a;
    font-size: 2.5rem;
    /* padding: 6% 15%; */
    text-align: center;
    /* margin: 0; */
    bottom: 35%;
    position: relative;
}

.answers-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    position: relative;
    /* top: 50%; */
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
    color: #ffffff;
    border-radius: 100px;
    padding: 20px 30px;

}

.pulse-button-hover:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}

.draggable-area {
    position: absolute;
    width: 18%;
    height: 65%;
    left: 40%;
    bottom: 20%;
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
}

.list-item {
    list-style: none;
    display: inline-block;
    padding: 8px 30px;
    margin: 10px;
    font-size: 1.2rem;
    font-weight: 500;
    position: relative;
    background: #02739f;
    cursor: pointer;
    border-radius: 30px;
    color: white;
    transition: all 0.3s ease;
    /* bottom: 15%; */
}

.text {
    position: absolute;
    bottom: 85%;
    left: 25%;
    font-size: 1.2rem;
    color: #5f5a5a;
    animation: floatAnimation 3s ease-in-out infinite;
}

.text:hover {
    color: #232020;
    cursor: pointer;
}

@keyframes floatAnimation {
    0% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-8px);
    }

    100% {
        transform: translateY(0);
    }
}

.list-item.dragging {
    transform: scale(0.8);
    /* Reduce the size of the item when dragging */
}

.list-item:hover {
    animation: borderPulse 1000ms infinite ease-out, hoverShine 200ms;
}

.word-warehouse {
    position: absolute;
    width: 88%;
    height: 10%;
    left: 5%;
    bottom: 8%;
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
}

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

.disabled {
    background-color: rgb(140, 139, 132);
    color: rgb(196, 194, 177);
    cursor: none;
}
</style>
