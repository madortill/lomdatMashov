<template>
    <div id = "end-screen">
        <h3>לסיכום</h3>
        <div class="finale-exe"> 

        </div>
    </div>
</template>

<script>

export default {
    name: 'end-screen',
    components: {
      
    },
    date() {
        return {

        };
    },
    methods: {

    },
}
</script>

<style>

#end-screen {
    background-color: #F2F2F2;
    width: 100%;
    height: 100vh;
    display: flex;
    position: relative;
    justify-content: center;
}

.finale-exe {
    position: absolute;
    width: 40%;
    height: 70%;
    left: 30%;
    bottom: 15%;
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
    text-align: center;
}
</style>
