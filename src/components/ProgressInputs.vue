<template>
  <div class="progressinputs">
    <div class="progressinputs__container">
      <span>Adjustable Variables</span>
      <form @submit="sendVariablesToParent">
        <p>Hexidecimal Color : {{color}}</p>
        <input type="color" name="fill-color" placeholder="Enter Hex" v-model="color">
        <p>Circle Size: {{size}}</p>
        <input
          class="progressinputs__slider"
          type="range"
          min="1"
          max="10"
          name="size"
          placeholder="Size"
          v-model="size"
        >
        <p>Starting Value: {{percentage}}%</p>
        <input
          class="progressinputs__slider"
          type="range"
          min="0"
          max="100"
          name="progress value"
          v-model="percentage"
        >
        <input class="progressinputs__button" type="submit" value="Submit">
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProgressInputs",
  data() {
    // Default circle data for component
    return {
      color: "#00add0",
      size: 5,
      percentage: 50
    };
  },
  methods: {
    sendVariablesToParent(e) {
      // Prevents Form submission refreshing page.
      e.preventDefault();

      // Object containing the parameters to send up to the parent.
      const newVariables = {
        color: this.color,
        size: this.size,
        percentage: this.percentage
      };

      //	Sends the inputted values up to the parent
      this.$emit("add-variables", newVariables);
    }
  }
};
</script>

<style scoped>
.progressinputs {
  width: 100%;
  padding: 50px 0;
}

.progressinputs__container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

span {
  width: 100%;
  padding: 10px;
  font-weight: 300;
  text-align: center;
  text-transform: uppercase;
}
form {
  width: 100%;
  max-width: 500px;
  display: flex;
  flex-wrap: wrap;
  padding: 50px;
  border: 1px solid black;
  border-radius: 3px;
}
input {
  width: 100%;
  height: 25px;
  cursor: pointer;
  margin: 5px 0;
}
input[type="submit"] {
  background-color: #d3d3d3;
  border: 1px solid black;
}
@media (max-width: 768px) {
  form {
    width: 70%;
  }
}
</style>
