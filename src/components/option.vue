<script setup>
import {ref,defineProps} from 'vue'
const {option,btn_color,option_selected} = defineProps(['option','btn_color','option_selected'])
</script>

<template>
 <button type="button" v-if="option.id==option_selected" class="btn  p-3 w-50 mt-2"   :class="btn_color" >{{option.content}}</button>   
 <button type="button" v-else class="btn btn-secondary p-3 w-50 mt-2"  :disabled="option_selected">{{option.content}}</button>   
</template>
<style scoped>
</style>