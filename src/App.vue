<template>
  <div class="result-display">
    <ResultDisplay :JSONQuestionsResults="JSONQuestionsResult" v-if="isShowingResults" @closeResult="closeResult"/>
  </div>
  <h1 class="title">Flashcard Game</h1>
  <div class="question-list">
    <QuestionsList ref="questionList"/>
  </div>
  <div class="flashcard-display">
    <FlashcardDisplay ref="flashcardDisplay" :currentQuestion="currentQuestion" @stardClicked="changeQuestion" />
  </div>
  <div class="flashcard-buttons">
    <FlashcardButtons v-if="isGameRunning" @buttonsClicked="(res)=>{mainButtonsHandler(res)}"/>
  </div>

</template>

<script>
  import QuestionsList from './components/QuestionsList.vue';
  import FlashcardDisplay from './components/FlashcardDisplay.vue'
  import FlashcardButtons from './components/FlashcardButtons.vue';
  import ResultDisplay from './components/ResultDisplay.vue';

  export default{
    data(){
      return{
        isGameRunning: false,
        isShowingResults: false,
        currentQuestion: "",
        JSONQuestionsResult: null,
        questionsResults: {
          "idk" : [],
          "s": [],
          "ik": [],
        },
      }
    },
    methods:{
      changeQuestion(){
        let questionListComponent = this.$refs.questionList;
        let questions = questionListComponent.questions;
        if (questions.length < 2){
          window.alert("There has to be at least 2 questions.");
          return;
        }
        this.$refs.flashcardDisplay.gameStarted = true;
        if(!this.isGameRunning){
          this.isGameRunning = true;
        }
        let newQuestion = questions[Math.floor(Math.random()*questions.length)];
        if (newQuestion == this.currentQuestion){
          this.changeQuestion();
        }else{
          this.currentQuestion = newQuestion;
        }
      },
      stopGame(){
        this.$refs.flashcardDisplay.gameStarted = false;
        this.isGameRunning = false;
        this.showResult();
        this.clearQuestionsResults();
      },
      mainButtonsHandler(res){
        if (res == "stop"){
          this.stopGame();
          return;
        }
        this.questionsResults[res].push(this.currentQuestion);
        this.changeQuestion();
      },
      clearQuestionsResults(){
        for (const key in this.questionsResults){
          this.questionsResults[key] = [];
        }
      },
      showResult(){
        this.JSONQuestionsResult = JSON.parse(JSON.stringify(this.questionsResults));
        this.isShowingResults = true;
      },
      closeResult(){
        this.JSONQuestionsResult = null;
        this.isShowingResults = false;
      }
    },
    components:{
      QuestionsList,
      FlashcardDisplay,
      FlashcardButtons,
      ResultDisplay
    }
  }
</script>

<style>
  @font-face{
    font-family: Poppins-regular;
    src: url("./Assets/Font/Poppins-Regular.ttf");
  }

  *{
    margin: 0;
    border: 0;
    padding: 0;
    box-sizing: border-box;
    word-wrap: break-word;
    cursor: default;
  }

  body{
    background-color: rgb(33, 33, 33);
    color: rgb(251, 255, 240);
    font-family: Poppins-regular, Verdana, Geneva, Tahoma, sans-serif;
    height: 100vh;
  }

  #app{
    height: 100%;
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-template-rows: repeat(6, 16.666666vh);
  }

  .title{
    grid-column: 3/ 8;
    grid-row: 1/ 2;
    align-self: center;
    justify-self: center;

    font-size: 3.5rem;
  }

  .question-list{
    grid-column: 1 / 3;
    grid-row: 1 / 7;
  }

  .flashcard-display{
    grid-column: 3 / 8;
    grid-row: 2 / 6;
    align-self: center;
    justify-self: center;
  }

  .flashcard-buttons{
    grid-column: 3 / 8;
    grid-row: 6 / 7;
    align-self: center;
  }

  button{
    cursor: pointer;
  }

</style>