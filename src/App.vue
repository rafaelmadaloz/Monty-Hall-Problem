<template>
    <div id="app">
        <h1>Monty Hall Problem</h1>
        <div class="form">
            <div v-if="!started">
                <label for="portsAmount">How many doors?</label>
                <input type="text" id="portsAmount" size="2"
                    v-model.number="portsAmount">
            </div>
            <button v-if="!started" @click="startGame">Start</button>
            <button v-if="started" @click="started = false">Reload</button>
        </div>

        <div class="doors" v-if="started">
            <div v-for="i in portsAmount" :key="i">
                <Door :hasGift=" i === selectedPort" :number="i" />
            </div>
        </div>
    </div>
</template>

<script>

import Door from './components/Door'

export default {
    name: 'App',
    components: { Door },
    data() {
        return {
            started: false,
            portsAmount: 3,
            selectedPort: null,
        }
    },
    methods: {
        startGame() {
            this.started = true
            this.selectedPort = parseInt(Math.random() * (this.portsAmount) + 1);
        }
    }
}
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Montserrat', sans-serif
    }

    body {
        background: linear-gradient(to right, rgb(121, 165, 231), rgb(54, 175, 223));
        color: white;
    }

    #app {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    #app h1 {
        border: 1px solid #000;
        background-color: #0004;
        padding: 20px;
        margin-bottom: 60px;
    }

    .form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-bottom: 40px;
    }

    .form, .form input, .form button {
        margin-bottom: 10px;
        font-size: 2rem;
    }

    .form input {
        width: 50px;
        margin-left: 10px;
        text-align: center;
    }

    .form button {
        margin-top: 30px;
    }

    .doors {
        margin-top: 40px;
        align-self: stretch;
        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }

    button {
        background-color: rgb(107, 204, 211);
        border-radius: 10px;
        color: white;
        border: solid 2px white;
        outline: none;
    }

</style>