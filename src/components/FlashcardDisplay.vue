<template>
    <div class="container">
        <button v-if="!gameStarted" @click="startClicked">Start</button>
        <p v-if="gameStarted">{{ currentQuestion.q }}</p>
    </div>
        
</template>

<script>
    export default{
        data(){
            return{
                gameStarted: false,
            }
        },
        methods:{
            // Cambiare in modo che mando solo il segnale che il tatso è stato premuto
            startClicked(){
                this.$emit("stardClicked");
            }
        },
        emits:[
            "stardClicked",
        ],
        props: [
            "currentQuestion",
        ]
    }
</script>


<style scoped>
    .container{
        --margin: 30px;

        box-sizing: border-box;
        padding: 50px;
        margin: var(--margin);
        /* margin-top: 0;  */
        height: calc(76.66666vh - var(--margin)*2);
        width: calc(70.5svw - (var(--margin) + 60px)*2);
        background-color: rgb(25, 25, 25);
        border-radius: 36px;

        display: grid;
        justify-items: center;
        align-content: center;
        overflow: hidden;
    }

    button{
        padding: 24px 40px;
        border-radius: 16px;
        font-size: 2.5rem;
        background-color: rgb(213, 213, 213);
    }

    p{
        font-size: 2rem;
        padding: 12px;
        background-color: rgb(44, 44, 44);
        border-radius: 20px;
    }
</style>