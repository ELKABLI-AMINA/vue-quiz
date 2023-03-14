<script setup>
import {defineProps} from 'vue'
const {score_info} = defineProps(['score_info'])
</script>

<template>

<div class=" text-center mt-4">
            <h3 style="color:rgb(8, 152, 119);">
                Congratulation 
            </h3> 
            <h5>Your score is  ({{score_info[0].score}}/{{ score_info[1] }})</h5>
        </div>
       

       <div class=" text-center mt-4">
        <button  @click="$emit('return-Instractions')" type="button" class="btn btn-warning">Return</button>
        <button @click="$emit('start-quiz')" type="button" class="btn btn-success ms-3">Re Start</button>
        <div v-for="question in score_info[0].incQuestions ">
            <h3> Q : {{ question.question }}</h3>
            <p> Answer : {{ question.answers.comment }}</p><br>
            </div>
        </div>
</template>
<style scoped>
</style>