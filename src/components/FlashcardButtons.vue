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

<style>

</style>