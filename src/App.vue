<script setup>
import {ref} from 'vue';
import BodyMassIndexForm from './components/BodyMassIndexForm.vue'

const bmi = ref('')
// the type of units the user should enter their height and weight in
// this should be either metric or american
const unitType = ref('metric');

// assigns the value of bmi to the calculated bmi value using the inputted height and weight values
const calculateBMI = (height, weight) => {
  // the switch case performs a different calculation depending on the type of units
  switch (unitType.value) {
    case 'metric':
      bmi.value = (weight/(height*height)).toFixed(2);
      break;
    case 'american':
      bmi.value = (weight / ( height * height ) * 703).toFixed(2);
      console.log('using american');
      break;
  }
}

</script>

<template>
  <div>
    <h1>Body Mass Index Calculator</h1>
    <input v-model="unitType" value="metric" id="metric-units" type="radio">
    <label for="metric-units">Metric Units</label>

    <input v-model="unitType" value="american" id="american-units" type="radio">
    <label for="american-units">American Units</label>
  </div>
  <BodyMassIndexForm v-on:stats-entered="calculateBMI" v-bind:units="unitType"/>
  <p v-if="bmi">Your BMI is: {{bmi}}</p>
</template>

<style scoped>

</style>
