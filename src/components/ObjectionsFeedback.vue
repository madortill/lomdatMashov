<template>
    <div id="objections-feedback">
        <div v-if="!showVideo" class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <div v-if = "indexInfo == 1"  class = "process-div">
            <div v-for="(item, index) in arrayProcess" :key="index">
                <p>{{ item }}</p>
            </div>
        </div>
        <div v-if="!showVideo">
            <button v-if="index > 0" class="prevBtn" @click="prevBtn">חזור</button>
            <button class="nextBtn" @click="nextBtn">המשך</button>
        </div>
        <div v-if="showVideo">
            <video-section @to-the-end = "toTheEnd"></video-section>
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
            subj: 4,
            arrayTitle: ['', 'תהליך הטיפול בהתנגדות במשוב', 'סירטונים'],
            arrayInfo: ['התנגדויות במשוב ב-ביטוי התנהגותי של הנחנך לאי רצונו או יכולתו להמשיך בתקשורת עם החונך.', 'תהליך הטיפול בהתנגדות'],
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
        toTheEnd() {
            // this.showVideo = false;
            this.$emit('move-to-next', this.showQ);
        }
    },
}
</script>

<style>
.process-div {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    padding: 2% 10%;
}
</style>
