<template>
    <div id = "feedback-call">
        <div class="div-text">
            <h2 class="title-text">{{ arrayTitle[indexTitle] }}</h2>
            <p class="info-text"> {{ arrayInfo[indexInfo] }} </p>
        </div>
        <button v-if = "index > 0" class="prevBtn" @click="prevBtn">חזור</button>
        <button class="nextBtn" @click="nextBtn">המשך</button>
    </div>
</template>

<script>

export default {
    name: 'feedback-call',
    components: {
      
    },
    data() {
        return {
            subj: 2,
            index: 0,
            arrayTitle: ['מבנה חלון גוהרי', 'מבנה שיחת המשוב', 'העלאת תופעות במשוב'],
            arrayInfo: ['עיקר שיחת המשוב היא התמקדות בחלק העיוור - מה שאנחנו מודעים אליו והנחנך לא.', 'שיטת הסנדוויץ' , 'איך עושים את זה?'],
            indexTitle: 0,
            indexInfo: 0,
            showQ: true,
        };
    },
    methods: {
        prevBtn() {
            if(this.index > 0) {
                this.index--;
            }
            if (this.indexTitle > 0 && this.indexInfo) {
                this.indexTitle--;
                this.indexInfo--;
            }
        },
        nextBtn() {
            this.index++;
            this.indexTitle++;
            this.indexInfo++;
            if(this.indexTitle === 3) {
                this.$emit('move-to-next', this.showQ);
            }
        },
    },
}
</script>

<style>

</style>
