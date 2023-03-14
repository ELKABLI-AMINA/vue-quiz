<script setup>
import Option from './option.vue';
import {defineProps,ref} from 'vue';
const {quiz} = defineProps(['quiz'])
const currentQuestion = ref(0)
const random = ref([])
const i = ref(0)
const done  = ref(false)
const newnum = ref(null);
const score = {score:0,incQuestions:[]}
const option_selected = ref(false)
const color = ref('btn-secondary')

const randoomQuestions =(max) =>{
for(i.value=1;i.value<=max;i.value++){
 newnum.value =  Math.floor(Math.random() * (max));
 while (random.value.includes(newnum.value)){
  newnum.value =  Math.floor(Math.random() * (max));
 }
 random.value.push(newnum.value);
}
}
randoomQuestions(quiz.length)
 const checkOption = (option_id)=>{
    option_selected.value=option_id
    if(quiz[random.value[currentQuestion.value]].answers.correct==option_id){
       score.score++
       color.value='btn-success'
    

    }else{
        color.value='btn-danger'
        score.incQuestions.push(quiz[random.value[currentQuestion.value]])

    }
 }
const nextQuestion = ()=>{
    if(currentQuestion.value!=quiz.length-1){
        currentQuestion.value++
        option_selected.value=false
    }
    else{
        done.value =true
    }
    
}

</script>
<template>
 <div class="container"> 
        <div  class="container mt-5">
                <div class="d-flex justify-content-center row">
                    <div class="col-md-10 col-lg-10">
                        <div class="border">
                            <div class="question bg-white p-3 border-bottom">
                                <div class="d-flex flex-row justify-content-between align-items-center mcq">
                                    <h4 style="color:rgb(8, 152, 119);"></h4><span>({{ currentQuestion }} of {{ quiz.length }})</span></div>
                            </div>
                            <div class="question bg-white p-3 border-bottom">
                                <div class="d-flex flex-row align-items-center question-title">
                                    <h3 class="text-danger">Q.</h3>
                                     <h5 class="mt-1 ml-2"> {{ quiz[random[currentQuestion]].question }}</h5>
                                </div>
                                <div class=" row justify-content-between">
                                    <Option v-for="option in quiz[random[currentQuestion]].options" :key="option.id" :option="option" @click="checkOption(option.id)" :btn_color="color" :option_selected="option_selected"></Option>
                                </div>
                            </div>
                            <div class="d-flex flex-row justify-content-between align-items-center p-3 bg-white"><button @click="$emit('return-home')" class="btn btn-primary d-flex align-items-center btn-danger" type="button"><i class="fa fa-angle-left mt-1 mr-1"></i>&nbsp;Exit</button>
                            
                                <button  v-if="done" class="btn btn-primary border-success align-items-center btn-success" type="button" @click="$emit('return-result',score)">View Result<i class="fa fa-angle-right ml-2"></i></button>
                                <button  v-else class="btn btn-primary border-success align-items-center btn-success" type="button" @click="nextQuestion" :disabled="!option_selected">Next<i class="fa fa-angle-right ml-2"></i></button></div>
                            </div>
                    </div>
                </div>
                </div>
 </div>
</template>

<style scoped>
</style>