<template>
    <div class="background-container">
        <div class="results-container">
            <span class="result-title">RESULTS</span>
            <ul class="score-container">
                <!-- [idk, s, ik] -->
                <li v-for="result, idx in formatResult()" :id="idx" class="score">
                    <span class="score-number">{{ result }}</span> <br>
                    {{ scoreText[idx] }} 
                </li>
            </ul>

            <button type="button" @click="closeResultWindow" class="close-button">
                Close
            </button>
        </div>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                scoreText: ["YOU DON'T KNOW", "YOU SKIPPED", "YOU KNOW"],
            }
        },
        methods:{
            formatResult(){
                let result = Array(0);

                let i = 0;
                for (const resultType in this.JSONQuestionsResults){
                    result[i] = this.JSONQuestionsResults[resultType].length;
                    i++;
                }
                
                return result
            },
            closeResultWindow(){
                this.$emit("closeResult")
            }
        },
        props:["JSONQuestionsResults"],
        emits:["closeResult"]
    }
</script>

<style scoped>
    li{
        list-style-type: none;
    }

    .background-container{
        position: absolute;
        inset: 0;
        background-color: rgba(0, 0, 0, 0.4);

        display: grid;

        padding: calc(50vh - 270px) calc(50vw - 400px);
    }

    .results-container{
        background-color: black;
        border-radius: 24px;
        padding: 24px;
        display: flex;
        flex-direction: column;
    }

    .result-title{
        font-size: 2.3rem;
    }

    .score-container{
        height: 80%;
        display: flex;
        justify-content: space-evenly;
        align-items: center;
    }

    .score{
        text-align: center;
        font-size: 1.7rem;
        font-weight: bolder;

        &:nth-child(1){
            color:red
        }
        &:nth-child(2){
            color:yellow
        }
        &:nth-child(3){
            color:green
        }
    }

    .score-number{
        font-size: 3.3rem;
        font-weight: normal;
    }

    .close-button{
        font-size: 1.7rem;
        padding: 12px;
        border-radius: 16px;
    }

</style>