<script setup>
import {ref} from 'vue'
import Quiz from './components/quiz.vue'
import Stepper from './components/stepper.vue'
import Instractions from './components/instructions.vue'
import Result from './components/Resultat.vue'
import  q from './data/quiz.json'
const quiz = ref(q) 
const fullScore = ref([])

const currentStep = ref(1)
const currentComponent = ref(Instractions)
const startQuiz = ()=>{
  currentComponent.value = Quiz
  currentStep.value = 2
}
const showresult = (score)=>{
  fullScore.value.push(score)
  fullScore.value.push(quiz.value.length)
  currentComponent.value =  Result
  currentStep.value = 3

}
</script>
<template>
   <header>
    <div class="row">
          <div class="col-xs-12 col-md-8 offset-md-2 block border" >
            <Stepper :currentStep="currentStep"/>   
            
          </div>
    </div>
  </header>
  <main class="">
    <div class="row ">
      <div class="col-xs-12 col-md-8 offset-md-2 block border" style="min-height: 70vh;">
        <component :is="currentComponent"  @start-quiz="startQuiz" :quiz="quiz" @return-result="showresult" :score_info="fullScore"/>
      </div>
   </div>
  </main>
</template>
<style scoped>
</style>
