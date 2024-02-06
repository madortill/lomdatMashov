<template>
    <div id="open-screen">
        <img src="@/assets/media/לוגו-סופי-לבן.png" alt="logo-white" class="logo-white">
        <h2 class="text-title">לומדת משוב</h2>
        <button class="btnNext" @click = "startTutorial"> התחל </button>
        <div class="animation-part">

        </div>
    </div>
</template>

<script>
export default {
    name: "open-screen",
    components: {

    },
    data() {
        return {

        };
    },
    methods: {
        startTutorial() {
            this.$emit('next-page');
        }
    },
};

</script>

<style scoped>
#open-screen {
    background-size: 100% 100%;
    direction: rtl;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #D9D9D9;
}

.logo-white {
    width: 30%;
}

.text-title {
    color: #A6A6A6;
    font-family: 'Heebo-Bold';
    font-size: xx-large;
    position: absolute;
    bottom: 25%;
    left: 25%;
}

.btnNext {
    position: absolute;
    border: none;
    cursor: pointer;   
    /* width: 12%; */
    height: 6%;
    left: 10%;
    bottom: 13%;
	font-size: 1rem;
	color: #ffffff;
	border-radius: 100px;
    background-color: #0492bd;
    min-width:12%;
    max-width: 20%;
}


.btnNext {
	animation: borderPulse 1000ms infinite ease-out;
}

.btnNext:hover,
.btnNext:focus {
	animation: borderPulse 1000ms infinite ease-out,  hoverShine 200ms;
}


/* Declare border pulse animation */
@keyframes borderPulse {
  0% {
    box-shadow: inset 0px 0px 0px 5px rgba(255, 255, 255,.4), 0px 0px 0px 0px rgba(255,255,255,1);
  }
  100% {
    box-shadow: inset 0px 0px 0px 3px rgba(117, 117, 255,.2), 0px 0px 0px 10px rgba(255,255,255,0);
  }
}

@keyframes hoverShine {
	0%{
		background-image: linear-gradient(135deg, rgba(255,255,255,.4) 0%, rgba(255,255,255,0) 50%, rgba(255,255,255,0) 100%);
	}
	50%{
		background-image: linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(255,255,255,.4) 50%, rgba(255,255,255,0) 100%);
	}
	100%{
		background-image: linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(255,255,255,0) 50%, rgba(255,255,255,.4) 100%);
	}
}

</style>