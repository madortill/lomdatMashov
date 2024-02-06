<template>
    <div id = "objections-feedback">
        <div v-if = "!showVideo" class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <button v-if = "index > 0"  class="prevBtn" @click="prevBtn">חזור</button>
        <button class="nextBtn" @click="nextBtn">המשך</button>
        <div v-if = "showVideo"> 
            <video-section :videoNum = "videoNum"></video-section>
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
            arrayTitle: [ '', 'תהליך הטיפול בהתנגדות במשוב', 'סירטונים'],
            arrayInfo: ['התנגדויות במשוב ב-ביטוי התנהגותי של הנחנך לאי רצונו או יכולתו הלמשיך בתקשורת עם החונך','תהליך הטיפול בהתנגדות'],
            indexTitle: 0,
            indexInfo: 0,
            showVideo: false,
            index: 0,
            videoNum: 0,
            showQ: true,
        };
    },
    methods: {
        prevBtn() {
            if(this.index > 0) {
                this.index--;
                this.indexTitle--;
                this.indexInfo--;
            }
            
            if(this.indexTitle <= 2) {
                this.showVideo = false;
                this.videoNum--;
                console.log(this.videoNum);
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;

            if(this.indexTitle > 3) {
                this.showVideo = true;
                this.videoNum++;
                console.log(this.videoNum);
            }

            if(this.indexTitle === 8) {
                this.$emit('move-to-next', this.showQ);
            }
        },
    },
}
</script>

<style>

</style>
