<template>
  <Screen>
    <div v-if="step === 'intro'" class="practice-instructions">
      <h2>Practice</h2>
      <p>
        You will now complete a short practice round to understand how the task works.
        Please select the object that you think the speaker is referring to.
      </p>
      <button @click="startPractice">Start practice</button>
    </div>

    <div v-if="step === 'trial'">
      <h2 class="utterance">{{ currentTrial.utterance }}</h2>

      <div class="grid-wrapper">
        <img :src="currentTrial.image" class="stimulus" />

        <button class="cell top-left" @click="selectObject('topLeft')" />
        <button class="cell top-right" @click="selectObject('topRight')" />
        <button class="cell bottom-left" @click="selectObject('bottomLeft')" />
        <button class="cell bottom-right" @click="selectObject('bottomRight')" />
      </div>
    </div>

    <div v-if="step === 'done'" class="practice-instructions">
      <h2>End of practice</h2>
      <p>
        The practice round is now complete. The real experiment will begin on the next screen.
      </p>
      <button @click="$magpie.nextScreen()">Continue</button>
    </div>
  </Screen>
</template>

<script>
export default {
  name: "PracticeBlock",
  props: {
    practiceTrials: Array
  },
  data() {
    return {
      step: "intro",
      trialIndex: 0
    };
  },
  computed: {
    currentTrial() {
      return this.practiceTrials[this.trialIndex];
    }
  },
  methods: {
    startPractice() {
      this.trialIndex = 0;
      this.step = "trial";
    },

    selectObject(cell) {
      const correctAnswers = Array.isArray(this.currentTrial.correctAnswer)
        ? this.currentTrial.correctAnswer
        : [this.currentTrial.correctAnswer];

      const isCorrect = correctAnswers.includes(cell);

      this.$magpie.addTrialData({
        trial_type: "practice_object_trial",
        trial_id: this.currentTrial.id,
        utterance: this.currentTrial.utterance,
        grey_cell: this.currentTrial.greyCell,
        response: cell,
        correct_answer: correctAnswers.join(","),
        correct: isCorrect
      });

      if (this.trialIndex < this.practiceTrials.length - 1) {
        this.trialIndex += 1;
        this.step = "trial";
      } else {
        this.step = "done";
      }
    }
  }
};
</script>

<style scoped>
.practice-instructions {
  width: 600px;
  margin: 0 auto;
  text-align: justify;
}

.practice-instructions h2 {
  text-align: center;
}

.practice-instructions button {
  display: block;
  margin: 20px auto;
}

.utterance {
  text-align: center;
  margin-bottom: 30px;
}

.grid-wrapper {
  position: relative;
  width: 500px;
  margin: 30px auto;
  line-height: 0;
}

.stimulus {
  width: 100%;
  display: block;
  margin: 0;
  padding: 0;
}

.cell {
  position: absolute;
  background: rgba(0, 0, 0, 0);
  border: 0;
  padding: 0;
  margin: 0;
  color: transparent;
  font-size: 0;
  appearance: none;
  -webkit-appearance: none;
  cursor: pointer;
}

.top-left {
  top: 0;
  left: 0;
  width: 50%;
  height: 50%;
}

.top-right {
  top: 0;
  left: 50%;
  width: 50%;
  height: 50%;
}

.bottom-left {
  top: 50%;
  left: 0;
  width: 50%;
  height: 50%;
}

.bottom-right {
  top: 50%;
  left: 50%;
  width: 50%;
  height: 50%;
}
</style>