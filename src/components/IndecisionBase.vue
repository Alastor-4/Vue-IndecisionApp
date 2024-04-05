<template>
    <img v-if="image" :src="image" alt="Background">

    <div class="indecision-container">
        <input v-model="question" type="text" placeholder="Hazme una pregunta">
        <p>Recuerda terminar con un signo de interrogación (?)</p>
    </div>

    <div v-if="isValidQuestion">
        <h2>{{ question }}</h2>
        <h1>{{ answer }}</h1>
    </div>
</template>

<script>
export default {
    data() {
        return {
            question: null,
            answer: null,
            image: null,
            isValidQuestion: false
        }
    },
    methods: {
        async getAnswer() {
            this.answer = "Pensando..."
            const { answer, image } = await fetch("https://yesno.wtf/api").then(r => r.json());

            switch (answer) {
                case "yes":
                    this.answer = "Si";
                    break;
                case "maybe":
                    this.answer = "Tal vez";
                    break;
                case "no":
                    this.answer = "No";
                    break;
                default:
                    break;
            }
            this.answer = answer;
            this.image = image;
        }
    },
    watch: {
        question(value) {
            this.isValidQuestion = false;
            if (!value.includes("?")) return;
            this.isValidQuestion = true;
            this.getAnswer();
        }
    }
}
</script>

<style scoped>
img {
    height: 100vh;
    left: 0px;
    max-height: 100%;
    max-width: 100%;
    position: fixed;
    top: 0px;
    width: 100vw;
}

.indecision-container {
    position: relative;
    z-index: 1;
}

input {
    width: 250px;
    padding: 10px 15px;
    margin: 25px 0;
    border-radius: 5px;
    border: none;
}

input:focus {
    outline: none;
}

p {
    color: white;
    font-size: 20px;
    margin-top: 0px;
}

h1,
h2 {
    color: white;
}

h2 {
    margin-top: 150px;
}
</style>