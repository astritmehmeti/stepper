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
  <div class="navigation-buttons">
    <button @click="goToPreviousStep" :disabled="activeStep === 1">
      Previous
    </button>
    <button @click="goToNextStep" :disabled="activeStep === steps.length">
      Next
    </button>
  </div>
</template>

<style>
.stepper-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 100vh;
  padding-left: 2vh;
  max-width: 100%;
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
  background-color: #007bff;
}

.title {
  margin-top: 1.4vh;
  margin-bottom: 1.4vh;
  text-align: center;
  color: #1d5795;
  font-weight: normal;
}

.title.active {
  font-weight: bold;
}

.title.done {
  font-weight: normal;
}

.line {
  width: 0.3vh;
  height: 6vh;
  margin-top: 7.2vh;
  background-color: #ccc;
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
  background-color: #007bff;
}

.step.done .line {
  background-color: #007bff;
}

@media (max-width: 1024px) {
  .stepper-container {
    padding-left: 2%;
  }

  .stepper {
    gap: 5.5vh;
  }

  .circle {
    width: 4vh;
    height: 4vh;
  }

  .title {
    margin-top: 1vh;
    margin-bottom: 1vh;
  }

  .line {
    width: 0.2vh;
    height: 5vh;
    margin-top: 6.2vh;
  }

  .step:not(:first-child) .line {
    margin-top: 8.2vh;
  }
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
  methods: {
    goToNextStep() {
      if (this.activeStep < this.steps.length) {
        this.activeStep++;
      }
    },
    goToPreviousStep() {
      if (this.activeStep > 1) {
        this.activeStep--;
      }
    },
  },
});
</script>

