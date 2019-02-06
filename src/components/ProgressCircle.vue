<template>
  <div class="progresscircle">
    <div class="progresscircle__container">
      <div class="progresscircle__box">
        <div
          class="progresscircle__circle"
          ref="circle"
          v-bind:style="{ height:scaleCircleRadius() + 'px', width:scaleCircleRadius() + 'px' }"
        >
          <div class="progresscircle__circle--load"></div>
        </div>
        <div class="progresscircle__text">
          <span
            v-bind:style="{ fontSize:scaleText() + 'px' }"
            ref="percentage"
          >{{inputVariables.percentage}}%</span>
        </div>
      </div>
      <div class="progresscircle__loaded">
        <span ref="loaded"></span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "ProgressCircle",
  props: ["inputVariables"],
  mounted() {
    // calls the circle animation function immediately upon component loading.
    this.animateCircle();
  },
  methods: {
    scaleCircleRadius() {
      // scales circle diameter
      return this.inputVariables.size * 25;
    },
    scaleText() {
      // scales text when circle diameter is increased or decreased
      return this.inputVariables.size * 4;
    },
    animateCircle() {

      var percent = this.inputVariables.percentage || 0;
      var backgroundColor = this.inputVariables.color || "#00add0";

      // Clears interval first incase of input change and removes 'Loading Complete'.
      clearInterval(this.setPercentageInterval);
      this.$refs.loaded.innerHTML = "";

      // sets an interval to increment the percentage number as well as the background visually at 50ms.
      this.setPercentageInterval = setInterval(() => {
        percent++;

        // Displays loaded text at 100%;
        if (percent == 100) {
          this.$refs.loaded.innerHTML = "Loading is complete";
        }

        if (percent <= 100) {
          // Changes percentage to scale with up.
          this.$refs.percentage.innerHTML = `${percent}%`;

          // loads background color slowly up.
          this.$refs.circle.style.background = `linear-gradient(to top, ${backgroundColor} ${percent}%,#fff ${percent}%,#fff 100%)`;

        }
      }, 50);
    }
  },
  watch: {
    inputVariables: function() {
      // Watches for change in the Input variables in the ProgressInputs file and animates again.
      this.animateCircle();
    }
  }
};
</script>

<style scoped>
.progresscircle {
  width: 100%;
  padding: 50px 0;
}

.progresscircle__container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  flex-direction: column;
}
.progresscircle__box {
  position: relative;
  display: flex;
  justify-content: center;
}

.progresscircle__text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #000;
}

.progresscircle__loaded {
  display: block;
  width: 100%;
  text-align: center;
  padding: 10px;
}

.progresscircle__circle {
  display: block;
  position: relative;
  height: 200px;
  width: 200px;
  border-radius: 100%;
  border: 3px solid;
}

.progresscircle__circle--load {
  border-radius: 100%;
  background: #fff;
  width: 0%;
  height: 100%;
}

span {
  width: 100%;
  text-transform: uppercase;
  text-align: center;
}
</style>
