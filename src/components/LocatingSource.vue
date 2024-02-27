<template>
    <div id="locating-source">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <div v-if="indexInfo === 0" class="original-container">
            <h2 class="textLS">המקור מכיל 3 מוקדים:</h2>
            <div v-for="(item, index) in arrayFocus" :key="index" class="circle-focus"
                :style="`--hue: ${index * 215 + 5}deg`">
                {{ arrayFocus[index] }}
            </div>
            <div v-for="(item, index) in arrayAction" :key="index" class="action-div">
                {{ arrayAction[index] }}
            </div>
        </div>

        <div v-if="indexInfo > 0" class="opatinSource">
            <h1>מקור התופעה</h1>
            <h1>הגדרת הבעיה</h1>
            <h1>שאלות אפשריות</h1>
            <h1>טיפול אפשרי</h1>
        </div>
        <div v-if="indexInfo > 0">
            <p class="loactingSource">{{ loactingSource[indexSource].name }}</p>
            <p>{{ loactingSource[indexSource].problem }}</p>
            <div v-for="(item, index) in loactingSource[indexSource].question" :key="index" class="loactingSource">
                <p>{{ item }}</p>
            </div>
            <div v-for="(item, index) in loactingSource[indexSource].treatment" :key="index" class="loactingSource">
                <p>{{ item }}</p>
            </div>
        </div>

        <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
        <button class="nextBtn" @click="nextBtn">המשך</button>
    </div>
</template>

<script>

export default {
    name: 'locating-source',
    components: {

    },
    data() {
        return {
            subj: 3,
            arrayTitle: [''],
            arrayInfo: ['כאשר הנך ממשב נחנך ומעיר על התנהגותו, עלייך לאבחן את מקור התופעה שלו.'],
            arrayFocus: ['מודעות', 'תפיסה', 'יישום'],
            arrayAction: ['הנחנך לא קלט את הגירוי.', 'פעולות הנחנך לא תואמות את התורה המקצועית.', 'בחירת פיתרון לא מתאים למצב'],
            loactingSource: [
                {
                    name: 'מודעות',
                    problem: 'החניך לא רואה את הבעיה ואינו מודע לה.',
                    question: [
                        'ראית ש...?',
                        'הרגשת ש...?',
                        'שמעת ש...?',
                    ],
                    treatment: [
                        'מתן הוכחות מהתצפית.',
                        'מתן כלים לתשומת לב.'
                    ]
                },
                {
                    name: 'תפיסה',
                    problem: 'החניך לא מבין למה זו בעיה.',
                    question: [
                        'מה את/ה חושב/ת על...?',
                        'האם את/ה מאמינ/ה ב...?',
                        'אך את/ה מתייחס ל...?',
                    ],
                    treatment: [
                        'טכניקות שיכנוע.',
                        'תיאור השלכות.',
                        'דיון ביתרונות וחסרונות.',
                        'דוגמאות מניסיון החונך.'
                    ]
                },
                {
                    name: 'יישום',
                    problem: 'החניך לא מצליח ליישם, אינו מוצא דרך לשנות את הבעיה.',
                    question: [
                        'איך עשית את...?',
                        'איזה שיטות נוספות את/ה מכיר/ה?',
                    ],
                    treatment: [
                        'הדגמה של פתרון.',
                        'תירגול.',
                        'מתן כלים נוספים.'
                    ]
                }
            ],
            indexTitle: 0,
            indexInfo: 0,
            index: 0,
            showQ: true,
            indexSource: -1,
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
                this.indexSource--;
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            this.indexSource++;
            if (this.indexTitle === 4) {
                this.$emit('move-to-next', this.showQ);
            }
        },
    },
}
</script>

<style>
.original-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 1rem;
    position: relative;
}

.circle-focus {
    width: 5rem;
    height: 6rem;
    border-radius: 50%;
    text-align: center;
    color: rgb(65, 63, 63);
    font-size: 2.5rem;
    font-weight: 550;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.3s ease;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
    background-color: hsl(var(--hue), 50%, 75%);
    position: fixed;
    padding: 3.5%;
    cursor: pointer;
}

.circle-focus:hover {
    width: 7rem;
    height: 8rem;
    box-shadow: 0 7px 9px rgba(0, 0, 0, 0.5);
}

.circle-focus:nth-child(2) {
    left: 20%;
    bottom: 35%;
}

.circle-focus:nth-child(3) {
    left: 52%;
    bottom: 35%;
}

.circle-focus:nth-child(4) {
    left: 85.5%;
    bottom: 35%;
}

.action-div {
    width: 13%;
    text-align: center;
    color: rgb(65, 63, 63);
    border-radius: 15px;
    font-size: 1.5rem;
    background-color: #e6e8e6;
    margin-top: 6%;
    padding: 1.5%;
    margin-right: 8%;
}

.textLS {
    position: fixed;
    bottom: 60%;
}

.opatinSource {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    padding: 2% 5%;
    /* flex-direction: column; */
}
</style>
