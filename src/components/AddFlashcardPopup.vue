<template>
    <div class="background-container" @keydown.{keyAlias}.enter.prevent="addingFlashcardHandler">
        <div class="popup-container">
            <h1>Add a new Flashcard</h1>
            <textarea type="text" v-model="flashCard"></textarea>
            <div class="buttons-container">
                <button @click="addingFlashcardHandler">
                    Add Flashcard
                </button>
                <button @click="closePopup">
                    Close
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                flashCard: "",
            }
        },
        methods: {
            addingFlashcardHandler(){
                if(this.flashCard == ""){
                    return;
                }
                this.$emit("flashCardAdded", this.flashCard);
                this.flashCard = "";
            },
            closePopup(){
                this.flashCard = "";
                this.$emit("popupClosing");
            }
        },
        emits: ["flashCardAdded", "popupClosing"]
    }
</script>

<style scoped>
    .background-container{
        position: absolute;
        height: 100%;
        width: 100%;
        background-color: rgba(0, 0, 0, 0.4);

        display: grid;
        justify-items: center;

        padding: calc(50vh - 200px) calc(50vw - 300px);
    }
    .popup-container{
        background-color: rgb(12, 102, 120);
        width: 100%;
        border-radius: 24px;
        padding: 24px;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
    }

    textarea{
        height: 50%;
        width: 100%;
        padding: 12px;
        resize: none;
        font-size: 1.1rem;
        border-radius: 16px;
    }

    button{
        padding: 22px;
        margin: 0 16px;

        border: 0;
        border-radius: 16px;

        font-size: 1.1rem;
    }
</style>