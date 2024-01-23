<template>
    <div id="information-page">
        <div class="div-text">
            <h2 class="title-text">מהו משוב?</h2>
            <p class="info-text">משוב הוא מידע על התנהגות בעבר, אשר נמסר בהווה ועשוי להשפיע על ההתנהגות בעתיד</p>
        </div>
        <button class="contBtn" @click = "nextInfo"> המשך </button>
    </div>
</template>

<script>

export default {
    name: 'information-page',
    data() {
        return {

        };
    },
    methods: {
        nextInfo() {
            this.$emit('next-info');
        }
    },
}

</script>

<style>

#information {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center; 
 }

 .div-text {
    width: 50%;
    height: 50%;
    background-color: #75ade2;
    border-radius: 10px;
 }
 
 .info-text {
    padding: 5%;
 }

 .title-text {
    padding: 5%;
 }

 .contBtn {
    background-color:#006998;
    position: absolute;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    cursor: pointer;   
    width: 9%;
    height: 6%;
    left: 10%;
    bottom: 13%;
    transition: background-color 0.3s linear;
 }

.contBtn:hover {
    background-color: #00A4E6;
}
 </style>
