<template>
    <div id="navbar">
        <div class="container">
            <nav>
                <ul>
                    <li>עקרונות יסוד</li>
                    <li>שיחת המשוב</li>
                    <li>איתור מקור התופעות</li>
                    <li>התנגדויות במשוב</li>
                </ul>
            </nav>
        </div>
        <information-page @next-info = "next"></information-page>
    </div>
</template>

<script>
import Information from '@/components/Information.vue';

export default {
    name: 'navbar',
    components: {
        Information
    },
    date() {
        return {

        };
    },
}
</script>

<style scoped>

#navbar {
    background-color: #F2F2F2;
}

* {
    margin: 0;
    box-sizing: border-box;
}

.container {
    height: 25vh;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    align-content: flex-start;
    flex-wrap: wrap;
    margin-top: 2%;
}

nav {
    background: #fff;
    border-radius: 50px;
    box-shadow: 0 15px 20px -20px rgba(0, 0, 0, 0.4);
}

nav ul li {
    padding: 0;
    list-style: none;
    display: inline-block;
    padding: 15px 35px;
    margin: 10px;
    font-size: 18px;
    font-weight: 500;
    color: #777;
    cursor: pointer;
    position: relative;
    z-index: 2;
    transition: color 0.5s;
}

nav ul li::after {
    content: "";
    background: #0296d0;
    width: 100%;
    height: 100%;
    border-radius: 30px;
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: -1;
    opacity: 0;
    transition: top 0.5s, opacity 0.5s;
}

nav ul li:hover {
    color: #fff;
}

nav ul li:hover::after {
    top: 50%;
    opacity: 1;
}

</style>
