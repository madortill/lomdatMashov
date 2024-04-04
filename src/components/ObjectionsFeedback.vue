<template>
    <div id="objections-feedback">
        <div v-if="!showVideo" :class="{ 'div-text-plus': indexTitle === 2, 'div-text': indexTitle !== 3 }">
            <h2 class="title-text" >{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
            <div v-if = "indexInfo == 2">
                <h1 style = "font-size: 2.5rem; position: relative">בהצלחה!</h1>
            </div>
        </div>
        <div v-if="indexInfo == 0">
            <img src="@/assets/media/OF/people.png" alt="people" class="people-img">
        </div>
        <div v-if="indexInfo == 1" class="process-div">
            <p class="click-me">לחצו עליי!</p>
            <div v-for="(item, index) in arrayProcess" :key="index" :id="index" class="process-item" @click="showItem"
                :style="`--hue: ${index * 17 + 180}deg`">
                <Transition>
                    <p v-show="indexArrayProcess >= index" class = "itemP">{{ item }}</p> 
                </Transition>
                <Transition>
                    <p v-show="showBackToMashov" class="back-mashov"> חזרה לשיחת משוב</p>  
                </Transition>
            </div>
        </div>
       
        <div v-if="!showVideo">
            <button v-if="index > 0 " class="prevBtn" @click="prevBtn">חזור</button>
            <button class="nextBtn" @click="nextBtn">המשך</button>
        </div>
        <div v-if="showVideo">
            <video-section @to-the-end="toTheEnd"></video-section>
        </div>
    </div>
</template>

<script>
import VideoSection from '@/components/VideoSection.vue';

export default {
    name: 'objections-feedback',

    components: {
        VideoSection,
    },
    data() {
        return {
            array: ['', '', '', ''],
            subj: 4,
            arrayTitle: ['', 'תהליך הטיפול בהתנגדות במשוב', 'סירטונים'],
            arrayInfo: ['התנגדויות במשוב ב-ביטוי התנהגותי של הנחנך לאי רצונו או יכולתו להמשיך בתקשורת עם החונך.', ' ', 'לפניכם קטע תירגול סימולצית סירטונים. תצטרכו לצפות בסירטון ולתאם את ההתנגדות שמופיע בסירטון.'],
            arrayProcess: [
                'זיהוי התנגדות',
                'עצירה ושיקוף',
                'איתור סיבת ההתנגדות',
                'טיפול בהתנגדות'
            ],
            indexTitle: 0,
            indexInfo: 0,
            showVideo: false,
            index: 0,
            showQ: true,
            indexArrayProcess: 0,
            showBackToMashov: false,
        };
    },
    methods: {
        prevBtn() {
            if (this.index > 0) {
                this.index--;
                this.indexTitle--;
                this.indexInfo--;
            }

            if (this.indexTitle <= 2 && this.videoNum > 0) {
                this.showVideo = false;
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            if (this.indexTitle > 2) {
                this.showVideo = true;
            }
        },
        showItem(event) {
            let itemBtn = event.currentTarget.id;
            console.log(itemBtn);
            this.indexArrayProcess++;
            if(this.indexArrayProcess === 4) {
                this.showBackToMashov = true;
            }
        },
        toTheEnd() {
            if(this.indexTitle === 3) {
                this.$emit('move-to-next', this.showQ);
            }
        }
    },
}
</script>

<style>
.process-div {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0%;
    position: relative;
}

.process-item {
    font-size: 1.6rem;
    width: 15%;
    border-radius: 50px;
    text-align: center;
    background-color: hsl(var(--hue), 50%, 60%);
    color: rgb(255, 255, 255);
    margin: 1%;
    transition: background-color 0.5s ease;
    box-shadow: 0 5px 7px rgba(0, 0, 0, 0.2);
}
.itemP {
    transition: color 0.3s ease;
}
.itemP:hover {
    cursor: pointer;
    color: rgb(0, 0, 0);
}

.process-item:hover {
    /* cursor: pointer; */
    background-color: hsl(var(--hue), 80%, 75%);
}

.people-img {
    width: 45%;
    position: absolute;
    top: 20%;
    left: 27%;
}

.back-mashov {
    position: absolute;
    bottom: 40%;
    left: 10%;
    font-size: 2.5rem;
    width: 20%;
    border-radius: 50px;
    text-align: center;;
    background-color: rgb(38, 214, 238);
    transition: background-color 0.5s ease;
    color: rgb(255, 251, 251);
    padding: 2%;
}

.process {
    position: absolute;
}

.v-enter-active,
.v-leave-active {
    transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}

.click-me {
    position: absolute;
    top: 0%;
    right: 35%;
    font-size: 1.2rem;
    color: #5f5a5a;
    animation: floatAnimation 3s ease-in-out infinite;
}

.div-text-plus {
    position: absolute;
    top:25%;
    width: 100%;
    height: 60%;
    text-align: center;
}

</style>
