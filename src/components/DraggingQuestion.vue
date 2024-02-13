<template>
    <div id="dragging-question">
        <div class="draggable-container">
            <h1 class="title-questionDragging">{{ this.questionInfo.title }}</h1>
            <p class="text"> * גרור את התשובה לפי הסדר המתאים.</p>
            <div class="draggable-area" @drop="(e) => {
                e.preventDefault();
                drop(e);
                checkDraggable(e)
            }" @dragover="allowDrop" id='dragArea' @dragstart="onDragging">
            </div>

            <div class="word-warehouse" @dragstart="onDragging" @dragover="allowDrop" @drop="(e) => {
                e.preventDefault();
                drop(e);
                checkDrop(e)
            }">
                <ul>
                    <li v-for="(item, index) in this.questionInfo.ansArray" :key="index"
                        class="list-item" draggable="true" @dragstart="drag" :id="'listItem' + index" :alt="'listItem' + index">
                        {{ item }} </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'dragging-question',
    props: ['questionInfo'],
    components: {

    },
    data() {
        return {
            answerArray: [],
          
        };
    },
    methods: {
        onDragging(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        },

        allowDrop(ev) {
            ev.preventDefault();
        },

        drag(ev) {
            ev.dataTransfer.setData("text", ev.target.alt);
        },

        drop(ev) {
            ev.preventDefault();
            const data = ev.dataTransfer.getData("text");
            // השתמשנו בקורנט טארגא במקום בטראגט בגלל שאנחנו רוצים להתייחס רק על האבא - יש מאזין של דראג שמשפיע על הילדים והמאזין של דרופ שמשפיע רק על האבא לכן נרצה לתפוס את המאזין לחיצה
            ev.currentTarget.appendChild(document.getElementById(data));
            // this.checkDraggable(data);
        },

        checkDraggable(ev) {
            const data = ev.dataTransfer.getData("text");
            let indexCorrectAns = 0;
            this.answerArray.push(data);
            const rightAns = this.questionInfo.rightAns;
            if (!rightAns) {
                console.log("rightAns is not defined or empty");
                return;
            }
            for (let i = 0; i < rightAns.length && i < this.answerArray.length; i++) {
                const newArrayElement = this.answerArray[i];
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
                        this.$emit('next-question')
                    }, 1500)
                }
            }
        },

        checkDrop(ev) {
            const data = ev.dataTransfer.getData("text");
            // console.log( this.newArray);
            for (let i = 0; i < this.answerArray.length; i++) {
                if (this.answerArray[i] === data) {
                    this.answerArray = this.answerArray.filter(item => item !== data);
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

.title-questionDragging {
    /* margin-bottom: 5%; */
    color: #5f5a5a;
    font-size: 2.5rem;
    /* padding: 6% 15%; */
    text-align: center;
    /* margin: 0; */
    bottom: 35%;
    position: relative;
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
    /* height: 10%; */
    left: 5%;
    bottom: 8%;
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
}

.correct {
    background-color: green;
}

.wrong {
    background-color: rgb(176, 6, 6);
}
</style>
