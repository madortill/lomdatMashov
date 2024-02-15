<template>
    <div id="video-section">
        <div class="video-container">
            <!-- המסכים לכאורה -->
            <div v-if="videoNum === 1" class="seemingly-agree">
                <iframe width="1000" height="650" src="https://www.youtube.com/embed/6LEmBHt4OCc?si=pvmt5NMR5PVC7tDL"
                    title="YouTube video player" frameborder="0"
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                    allowfullscreen>
                </iframe>
            </div>
            <!-- יהיר -->
            <div v-if="videoNum === 2" class="arrogant">
                <iframe width="1000" height="650" src="https://www.youtube.com/embed/LnEiYw9kgLg?si=0aImkNJLdEaAe-Hw"
                    title="YouTube video player" frameborder="0"
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                    allowfullscreen>
                </iframe>
            </div>
            <!-- טרגי -->
            <div v-if="videoNum === 3" class="tragic">
                <iframe width="1000" height="650" src="https://www.youtube.com/embed/h5WEL8XvM-4?si=y4qyrzHOoHguOvI3"
                    title="YouTube video player" frameborder="0"
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                    allowfullscreen>
                </iframe>
            </div>
            <!-- הווכחן -->
            <div v-if="videoNum === 4" class="argues">
                <iframe width="1000" height="650" src="https://www.youtube.com/embed/ogeQ033gZmg?si=lf8K6UwKx2tKeMqF"
                    title="YouTube video player" frameborder="0"
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                    allowfullscreen>
                </iframe>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'video-section',
    props: ["videoNum"],
    components: {

    },
    data() {
        return {
            // showViedo: 1,
        };
    },
    mounted() {
        // console.log('Video number:', this.videoNum);
    },
    methods: {
        // changeVideo() {
        //  this.showViedo = videoNum;
        // }   
    },
}
</script>

<style>
#video-section {
    display: flex;
    justify-content: center;
    align-items: center;
    /* height: 100vh; */
}

.video-container {
    margin-bottom: 15%;
}


</style>
