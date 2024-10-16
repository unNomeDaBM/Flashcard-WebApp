<template>
    <div class="background-container">
        <div class="results-container">
            <span class="result-title">RESULTS</span>
            <div class="questions-container">
                <ul>
                    <li>
                        {{ formatResult() }}
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        data(){
            return{
            }
        },
        methods:{
            formatResult(){
                let result;
                
                for (const answerType in this.JSONQuestionsResults){
                    //TODO: all the formatting of the answers
                }
                return result
            }
        },
        props:["JSONQuestionsResults"]
    }
</script>

<style scoped>
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
    }

    .result-title{
        font-size: 2.3rem;

    }

</style>