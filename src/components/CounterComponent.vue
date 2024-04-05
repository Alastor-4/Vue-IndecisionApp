<script setup>
defineProps({
    msg: {
        type: String,
        required: true,
    },
    start: {
        type: Number,
        default: 101,
        required: false,
        validator(value) {
            return value > 100
        }
    }
});
</script>

<template>
    <h2>{{ customMsg || "Counter" }}</h2>
    <p>{{ counter }}<sup>2</sup> = {{ squareCounter }}</p>
    <div>
        <button @click="incrementValue">+1</button>
        <button @click="decrementValue">-1</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            counter: this.start || 1
        }
    },
    methods: {
        getSquareValue() {
            return this.counter * this.counter;
        },
        incrementValue() {
            this.counter++;
        },
        decrementValue() {
            this.counter--;
        }
    },
    computed: {
        customMsg() {
            return this.counter || "Counter";
        },
        squareCounter() {
            return this.counter * this.counter;
        }
    }
}
</script>

<style>
button {
    background-color: #64B687;
    border-radius: 5px;
    border: 1px solid white;
    color: white;
    cursor: pointer;
    margin: 0 5px;
    padding: 5px 15px;
    transition: 0.3s ease-in-out;
}

button:hover {
    background-color: #5AA67B;
    transition: 0.3s ease-in-out;
}
</style>