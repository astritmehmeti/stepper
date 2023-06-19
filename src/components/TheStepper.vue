<template>
  <div class="stepper-container">
    <div class="stepper">
      <div
        v-for="(step, index) in steps"
        :key="index"
        :class="[
          'step',
          { active: index + 1 === activeStep },
          { done: index + 1 < activeStep },
        ]"
      >
        <div class="circle" :class="{ active: index + 1 <= activeStep }">
          {{ index + 1 }}
        </div>
        <div class="title" :class="{ active: index + 1 === activeStep }">
          {{ step }}
        </div>
        <div v-if="index !== steps.length - 1" class="line"></div>
      </div>
    </div>
  </div>
</template>

<style>
.stepper-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 100vh;
  padding-left: 2vh;
}

.stepper {
  display: flex;
  flex-direction: column;
  gap: 5.5vh;
}

.step {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.circle {
  width: 5vh;
  height: 5vh;
  border-radius: 50%;
  background-color: #ccc;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
}

.circle.active {
  background-color: #007bff; /* Set blue color for active circles */
}

.title {
  margin-top: 1.4vh;
  margin-bottom: 1.4vh;
  text-align: center;
  color: #1d5795; /* Set the blueish color for the text */
  font-weight: normal; /* Set the default font weight */
}

.title.active {
  font-weight: bold; /* Set the font weight to bold for the active step */
}

.title.done {
  font-weight: normal; /* Set the font weight back to normal for done steps */
}

.line {
  width: 0.3vh;
  height: 6vh;
  margin-top: 7vh;
  background-color: #ccc; /* Set the color to gray for the lines */
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  z-index: -1;
}

.step:first-child .line {
  top: 50%;
  transform: translateX(-50%) translateY(-50%);
}

.step:not(:first-child) .line {
  top: 0;
  bottom: 0;
  margin-top: 9.6vh;
}

.step.done .circle {
  background-color: #007bff; /* Set blue color for done circles */
}

.step.done .line {
  background-color: #007bff; /* Set blue color for done lines */
}
</style>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      steps: [
        "Stay Information",
        "Rooms & Add Ons",
        "Guest Information",
        "Guarantee Information",
        "Review & Book",
      ],
      activeStep: 3,
    };
  },
});
</script>
