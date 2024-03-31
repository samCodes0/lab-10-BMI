<script setup>
import { ref } from 'vue'

// defining the properties that will be passed from app.vue
defineProps({
  units: String
})
// define the messages that this component may send to other components
const emit = defineEmits([
  'statsEntered' // this message will be sent when the user enters their data
]);

// height and weight inputted by the user
const height = ref(0);
const weight = ref(0);

// the function will be called when the calculate button is pressed
function statsEntered() {
  // sending the data to app.vue
  emit('statsEntered', height.value, weight.value);
}

</script>

<template>
  <div id="form">
    <!-- Putting the labels and inputs into a table to make them aligned -->
    <table>
      <tr>
        <td><label for="height-input">Height
          <!-- Using the v-if and v-else-if directives to choose different spans
           displaying either meters or inches -->
          <span v-if="units === 'metric'">(in meters)</span>
          <span v-else-if="units === 'american'">(in inches)</span></label></td>
        <td><input id="height-input" v-model="height" type="number"></td>
      </tr>
      <tr>
        <td><label for="weight-input">Weight
          <!-- Doing the same thing except with kilograms and pounds -->
          <span v-if="units === 'metric'">(in kilograms)</span>
          <span v-else-if="units === 'american'">(in pounds)</span></label></td>
        <td><input id="weight-input" v-model="weight" type="number"></td>
      </tr>
    </table>
    <br>
    <button v-on:click="statsEntered">Calculate</button>
  </div>

</template>

<style scoped>
  table {
    /* making sure the table appears centered */
    margin: auto;
  }
</style>
