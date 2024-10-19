<template>  
    <AddFlashcardPopup v-if="popupVisibility" 
    @flashCardAdded="(f)=>{addingFlash(f)}"
    @popupClosing="popupVisibility = !popupVisibility;"/>

    <div class="container">
        <h1>
            QUESTIONS
        </h1>

        <ol>
            <li v-if="questions.length == 0" class="placeholderQuestion">Ancora nessuna domanda aggiunta...</li>
            <li v-for="question in questions" :key="question.id" :class="questionsVisibility    ">
                {{ question.q }} 
                <br>
                <span class="delete-x" @click="deleteFlash(question.id)">X</span>
            </li>
        </ol>

        <button class="first" @click="popupVisibility = !popupVisibility">
            Add a new Flashcard
        </button>
        <button @click="changeQuestionVisibility">
            Hide questions
        </button>
    </div>

</template>

<script>
    import AddFlashcardPopup from './AddFlashcardPopup.vue';

    export default {
        components:{
            AddFlashcardPopup,
        },
        data(){
            return{
                questions: [],
                questionsVisibility: "",
                popupVisibility: false,
                idCounter: 2,
            }
        },
        methods: {
            getFlashcardId(){
                return this.idCounter++;
            },
            addingFlash(f){
                this.questions.push({q: f, id: this.getFlashcardId()});
            },
            deleteFlash(key){
                this.questions.forEach((question, indx)=>{
                    if(question.id == key){
                        this.questions.splice(indx, 1);
                        return;
                    }
                })
            },
            changeQuestionVisibility(){
                if (this.questionsVisibility == ""){
                    this.questionsVisibility = "invisibleQuestion";
                }else if (this.questionsVisibility == "invisibleQuestion"){
                    this.questionsVisibility = "";
                }
            }
        },
    }
</script>

<style scoped>
    h1{
        padding-bottom: 6px;
    }

    .container{
        background-color: #484848;
        margin: 50px 50px;
        padding: 24px;
        height: calc(100vh - 100px);
        border-radius: 24px;

        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    ol{
        list-style: none;
        background-color: rgb(58, 58, 58);
        height: 80%;
        border-radius: 16px;
        padding: 6px;
        overflow-y: scroll;
    }
    li{
        background-color: rgb(95, 95, 95);
        padding: 8px 12px 8px 8px;
        border-radius: 12px;
        margin: 6px 0;
        
        &:last-child{
            margin: 6px 0 0 0;
        }
        &:first-child{
            margin: 0 0 6px 0;
        }
    }
    .delete-x{
        color: rgb(200, 34, 34);
        font-weight: bolder;
        height: 0px;
        user-select: none;
        cursor: pointer;
    }

    button{
        font-size: 1.2rem;
        padding: 8px;
        border-radius: 8px;
        
        margin: 4px 0;
    }
    button, .first{
        margin: 8px 0 0 0;
    }

    .invisibleQuestion{
        color: rgba(0, 0, 0, 0);
    }

    ::-webkit-scrollbar {
        width: 5px;
    }
    ::-webkit-scrollbar-track {
        background: #888; 
    }
    
    ::-webkit-scrollbar-thumb {
        background: #f1f1f1; 
        border-radius: 3px;
    }

    ::-webkit-scrollbar-thumb:hover {
      background: #3bbc93; 
    }
</style>