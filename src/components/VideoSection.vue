<template>
  <div id="video-section">
    <div class="video-container">
      <!-- המסכים לכאורה -->
      <div v-if="videoNum === 0" class="seemingly-agree">
        <video width="900" height="550" controls>
          <source src="../assets/media/videos/מקרה 1 - מדור טיל - קריית ההדרכה (1080P50, H264, Youtube).mp4" type="video/mp4" />
        </video>
      </div>
      <!-- יהיר -->
      <div v-if="videoNum === 1" class="arrogant">
        <video width="900" height="550" controls>
          <source src="../assets/media/videos/מקרה 2 - מדור טיל - קריית ההדרכה (1080P, H264, Youtube).mp4" type="video/mp4" />
        </video>
      </div>
      <!-- טרגי -->
      <div v-if="videoNum === 2" class="tragic">
        <video width="900" height="550" controls>
          <source src="../assets/media/videos/מקרה 3 - מדור טיל - קריית ההדרכה (1080P, H264, Youtube).mp4" type="video/mp4" />
        </video>
      </div>
      <!-- הווכחן -->
      <div v-if="videoNum === 3" class="argues">
        <video width="900" height="550" controls>
          <source src="../assets/media/videos/מקרה 4 - מדור טיל - קריית ההדרכה (1080P, H264, Youtube).mp4" type="video/mp4" />
        </video>
      </div>
    </div>
    <p v-if="!showInfo" class="text-objection">איזו התנגדות זיהית בסירטון?</p>
    <div v-if="!showInfo" class="btn-container">
      <button
        v-for="(button, index) in this.shuffledArr"
        :key="index"
        class="btnVideo"
        :id="index"
        :ref="index"
        @click="checkAnswer"
      >
        {{ button }}
      </button>
    </div>
    <div v-if="showInfo" class="video-information">
      <video-information
        :indexObjection="indexObjection"
        @next-video="nextVideoSection"
      ></video-information>
    </div>
  </div>
</template>

<script>
import VideoInformation from "@/components/VideoInformation.vue";

export default {
  name: "video-section",
  components: {
    VideoInformation,
  },
  data() {
    return {
      buttons: ["המסכים לכאורה", "היהיר", "הטרגי", "הווכחן"],
      correctArray: ["המסכים לכאורה", "היהיר", "הטרגי", "הווכחן"],
      correctAnswer: 0,
      player: null,
      showInfo: false,
      indexObjection: 0,
      videoNum: 0,
    };
  },
  computed: {},
  mounted() {
    window.onYouTubeIframeAPIReady = this.initVideo;
  },
  methods: {
    initVideo() {
      this.player = new YT.Player("player", {
        height: "550",
        width: "900",
        videoId: "6LEmBHt4OCc",
        playerVars: {
          controls: "0",
        },
        events: {
          onReady: this.onPlayerReady,
          onStateChange: this.onPlayerStateChange,
        },
      });
    },
    onPlayerReady(event) {
      console.log("dhsdh");
      event.target.playVideo();
    },
    onPlayerStateChange(event) {
      console.log("dhsdh");
      if (event.data === 0) {
        alert("done");
      }
    },
    checkAnswer(event) {
      let btnAnswer = event.currentTarget.textContent;
      if (btnAnswer === this.correctArray[this.videoNum]) {
        this.indexObjection = this.videoNum;
        event.target.classList.add("correct");
        setTimeout(() => {
          this.showInfo = true;
        }, 1500);
      } else {
        event.target.classList.add("wrong");
        this.showInfo = false;
      }
    },

    checkVideo(event) {
      console.log(event.target.className);
      console.log("dfvdsfc");
    },
    nextVideoSection(event) {
      this.videoNum++;
      this.showInfo = false;
      this.buttons = this.shuffledArr;
      if (this.videoNum > 3) {
        this.$emit("to-the-end");
      }
    },
  },
  computed: {
    shuffledArr() {
      let returnArray = this.buttons.slice(); // שכפול מערך התשובות הנכונות
      let tmp = this.buttons.slice();
      for (let i = 0; i < returnArray.length; i++) {
        let index = Math.floor(Math.random() * tmp.length);
        returnArray[i] = tmp[index];
        tmp = tmp.slice(0, index).concat(tmp.slice(index + 1)); // removes tmp[index]
      }
      return returnArray;
    },
  },
};
</script>

<style>
#video-section {
  display: flex;
  justify-content: center;
  align-items: center;
}

.video-container {
  margin-bottom: 15%;
}

.btn-container {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 15%;
  margin: 0 20px;
}

.btnVideo {
  background-color: #047fb0;
  margin: 0 2rem;
  cursor: pointer;
  border: none;
  font-size: 1.5rem;
  color: #ffffff;
  border-radius: 100px;
  padding: 20px 30px;
}

.btnVideo:hover {
  animation: borderPulse 4000ms infinite ease-out, hoverShine 200ms;
}

.text-objection {
  position: absolute;
  bottom: 25%;
  font-size: 1.3rem;
  color: #5f5a5a;
}

.correct {
  background-color: green;
}

.wrong {
  background-color: rgb(176, 6, 6);
}

/* .disabledBtnVideo {
    background-color: rgb(224 224 223);
    color: rgb(255, 255, 255);
    cursor: default;
} */

.video-information {
  position: absolute;
  bottom: 10%;
}
</style>
