<template>
  <v-choice v-model="choiceModel" name="group1" :options="options" :multiple="flag" @CheckItem="check"
    label="Radio Group" />
    <button @click="Change()">Change Type</button>
  <ul>
  <li v-for="(item,index) in choiceModel" :key="index">
    {{item}}
  </li>
  </ul>
  
</template>

<script setup lang="ts">
import { ref } from 'vue';
import VChoice from '@/components/VChoice.vue'

const flag = ref(true)
const choiceModel = ref([])

const options = [
  { text: "Option 1", value: "a" },
  { text: "Option 2", value: "b" },
  { text: "Option 3", value: "c" },
]
const Change = ()=>{
  flag.value = !flag.value
  choiceModel.value = []
}

const newIndex = ref('')
const check = (item, type) => {
  if (type) {
    if (!choiceModel.value.includes(item)) {
      choiceModel.value.push(item)
    }
    else {
      newIndex.value = choiceModel.value.indexOf(item)
      choiceModel.value.splice(newIndex.value, 1)
    }
  }
  else {
    choiceModel.value = []
    choiceModel.value.push(item)
  }

}
</script>

<style scoped></style>
