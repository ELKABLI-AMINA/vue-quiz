<script setup>
import {defineProps} from 'vue';
const {currentStep} = defineProps(['currentStep'])
const steps = 3
const stepsNames = ['Instractions','Quiz','Results']
</script>

<template>
<div class="wrapper-progressBar">
      <ul class="progressBar">
         <li v-for="(step, index) in steps" :key="index" :class="{ active: currentStep >=step  }" >{{ stepsNames[step-1] }}</li>
      </ul>
 </div>
</template>
<style scoped>

.wrapper-progressBar {
    width: 100%
}
.progressBar li {
    list-style-type: none;
    float: left;
    width: 33%;
    position: relative;
    text-align: center;
}

.progressBar li:before {
    content: " ";
    line-height: 30px;
    border-radius: 50%;
    width: 30px;
    height: 30px;
    border: 1px solid #ddd;
    display: block;
    text-align: center;
    margin: 0 auto 10px;
    background-color: white
}

.progressBar li:after {
    content: "";
    position: absolute;
    width: 100%;
    height: 4px;
    background-color: #ddd;
    top: 15px;
    left: -50%;
    z-index: -1;
}

.progressBar li:first-child:after {
    content: none;
}

.progressBar li.active {
    color: rgb(228, 168, 49);
}

.progressBar li.active:before {
    border-color: rgb(228, 168, 49);
    background-color:  rgb(228, 168, 49);
}

.progressBar .active:after {
    background-color:  rgb(228, 168, 49);
}
</style>