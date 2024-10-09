<template>
    <div class="container">
        <button @click="buttonClicked('idk')">
            I don't know
        </button>
        <button @click="buttonClicked('s')">
            Skip
        </button>
        <button @click="buttonClicked('ik')">
            I know
        </button>
        <button @click="buttonClicked('stop')">
            See results
        </button>
    </div>
</template>

<script>
    export default{
        data(){
            return{

            }
        },
        methods:{
            buttonClicked(res){
                this.$emit("buttonsClicked", res);
            }
        },
        emits:[
            "buttonsClicked",
        ] 
    }
</script>

<style scoped>
    .container{
        display: flex;
        justify-content: space-between;
        margin: 0 200px;
    }

    button{
        padding: 24px 32px;
        border-radius: 20px;
        font-size: 1.2rem;
        color: inherit;
        font-family: inherit;

        &:nth-child(1){
            background-color: rgb(151, 13, 13);
        }
        &:nth-child(2){
            background-color: rgb(159, 159, 36);
        }
        &:nth-child(3){
            background-color: rgb(36, 137, 13);
        }
        &:nth-child(4){
            background-color: rgb(116, 116, 116);
        }
    }
</style>