<template>
    <div id="quick-questions">
        <multiple-question v-if="questionToPass.Qtype === 0" @next-question="updateIndex"
            :questionInfo="questionToPass"></multiple-question>
        <dragging-question v-else="questionToPass.Qtype === 1" :key="questionToPass" @next-question="updateIndex"
            :questionInfo="questionToPass"></dragging-question>
    </div>
</template>

<script>
// import Draggable from 'vuedraggable';
import MultipleQuestion from '@/components/MultipleQuestion.vue';
import DraggingQuestion from '@/components/DraggingQuestion.vue';


export default {
    name: 'quick-questions',
    props: ['indexQuestion'],
    components: {
        DraggingQuestion,
        MultipleQuestion
    },
    data() {
        return {
            typeQuestion: 0,
            indexQ: 0,
            questions1: [
                {
                    Qtype: 0,
                    title: "לפי מודל חלון גוהרי, באיזה אחד מהחלקים שיחת המשוב תתמקד?",
                    ans1: "בחלון הגלוי",
                    ans2: "בחלון העיוור",
                    ans3: "בחלון הנסתר",
                    ans4: "בחלון הלא מודע",
                    correctAnswer: 2,
                },
                {
                    Qtype: 1,
                    title: "לפי שיטת הסנדוויץ, מה המבנה העקרוני של שיחת המשוב?",
                    correctArray: [
                        "יצירת חוזה",
                        "מתן ביטוי לנחנך",
                        "איסוף מידע חסר",
                        "העלאת תופעה לשימור",
                        "העלאת 2-3 תופעות לשיפור",
                        "העלאת תופעה נוספת לשימור",
                        "סיכום המשוב"
                    ],
                }, {
                    Qtype: 1,
                    title: "מנה/י\" 4 כללים שעליהם נותן המשוב חייב להקפיד.",
                    correctArray: [
                        "העלאת תיאור ההתנהגות",
                        "ציון דוגמאות",
                        "איתור סיבת התופעה",
                        "הסבר על תרומת ההתנהגות",
                    ],
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
                },
                {
                    Qtype: 1,
                    title: "סדר/י 3 שאלות למוקד המודעות.",
                    correctArray: [
                        "ראית ש...?",
                        "הרגשת ש...?",
                        "שמעת ש...?",
                    ],
                },
            ],

            questions3: [
                {
                    Qtype: 0,
                    title: "במהלך משוב שמת לב כי המפקד שמולך נמרח על הכיסא ולא מרוכז. כיצד תמשיך/י את שיחת המשוב?",
                    ans1: "שאילת שאלות",
                    ans2: "עצירה ושיקוף",
                    ans3: "להמשיך כרגיל",
                    ans4: "תדווח למפקד שלו",
                    correctAnswer: 2,
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
                    title: "במידה ובמהלך התמודדות עם התנגדויות שיקפת ושאלת שאלות כלליות והתנהגות הנחנך לא השתנתה, כיצד תמשיך/י את ההתמודדות?",
                    ans1: "ויכוח עם הנחנך",
                    ans2: "שאילת שאלות ספציפיות",
                    ans3: "שיקוף",
                    ans4: "עצירת המשוב",
                    correctAnswer: 4,
                },
            ]
        };
    },
    methods: {
        updateIndex() {
            if (this.indexQ < this[`questions${this.indexQuestion}`].length - 1) {
                this.indexQ++;
            } else {
                this.indexQ = 0;
                this.$emit('next-sub');
            }
        }
    },
    computed: {
        questionToPass() {
            return (
                this[`questions${this.indexQuestion}`][this.indexQ]
            )
        }
    }
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
</style>
