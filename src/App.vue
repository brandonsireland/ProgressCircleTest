<template>
  <div id="app">
    <Header />
    <!-- :inputVariables sends the new variables from the progress Inputs to the circle component -->
    <ProgressCircle :inputVariables="newVariables"/>
    <!-- 'v-on' Listens to child component event -->
    <ProgressInputs v-on:add-variables="newVariables = $event"/>
  </div>
</template>

<script>

// Importing Components to be used in main div.
import Header from './components/layout/Header';
import ProgressCircle from './components/ProgressCircle';
import ProgressInputs from './components/ProgressInputs';

export default {
  name: 'app',
  components: {
    Header,
    ProgressCircle,
    ProgressInputs
  },
  data(){
    return {
      // default values
        newVariables: {
          color: '#00add0',
          size: 5,
          percentage: 50
        }
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
