<template>
    <div id = "locating-source">
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
    name: 'locating-source',
    components: {
      
    },
    data() {
        return {
            subj: 3,
            arrayTitle: [ ''],
            arrayInfo: ['מודעות','תפיסה','יישום' ],
            indexTitle: 0,
            indexInfo: 0,
            index: 0,
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
