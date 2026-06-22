<template>
  <Screen>
    <div class="block-row">
      <div
        v-for="(trial, index) in block"
        :key="trial.id"
        class="trial-slot"
        :class="{ hidden: index > currentGrid }"
      >
        <h3 class="utterance">{{ trial.utterance }}</h3>

        <div class="grid-wrapper">
          <img :src="trial.image" class="stimulus" />

          <button
            class="cell top-left"
            :disabled="index !== currentGrid || hasResponse(index)"
            @click="selectCell('topLeft')"
          />
          <button
            class="cell top-right"
            :disabled="index !== currentGrid || hasResponse(index)"
            @click="selectCell('topRight')"
          />
          <button
            class="cell bottom-left"
            :disabled="index !== currentGrid || hasResponse(index)"
            @click="selectCell('bottomLeft')"
          />
          <button
            class="cell bottom-right"
            :disabled="index !== currentGrid || hasResponse(index)"
            @click="selectCell('bottomRight')"
          />

          <div
            v-if="responses[index]"
            class="selection-marker"
            :class="responses[index].response"
          />
        </div>
      </div>
    </div>
  </Screen>
</template>

<script>
export default {
  name: "GridTrial",
  props: {
    block: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      currentGrid: 0,
      blockStartTime: null,
      gridStartTime: null,
      responses: []
    };
  },
  mounted() {
    this.blockStartTime = performance.now();
    this.gridStartTime = performance.now();
  },
  methods: {
    hasResponse(index) {
      return Boolean(this.responses[index]);
    },

    selectCell(answer) {
      const now = performance.now();
      const trial = this.block[this.currentGrid];

      this.responses[this.currentGrid] = {
        trial_id: trial.id,
        phase: trial.phase,
        block_id: trial.block_id,
        trial_in_block: trial.trial_in_block,
        condition: trial.condition,
        utterance: trial.utterance,
        grey_cell: trial.greyCell,
        correct_answer: trial.correctAnswer,
        response: answer,
        correct: answer === trial.correctAnswer,
        rt: now - this.gridStartTime
      };

      if (this.currentGrid < this.block.length - 1) {
        this.currentGrid += 1;
        this.gridStartTime = performance.now();
      } else {
        this.finishBlock(now);
      }
    },

    finishBlock(endTime) {
      const blockRT = endTime - this.blockStartTime;
      const blockID = this.block[0].block_id;
      const phase = this.block[0].phase;

      const trialData = {
        phase,
        block_id: blockID,
        block_rt: blockRT,
        block_responses_json: JSON.stringify(this.responses)
      };

      this.responses.forEach((r, i) => {
        const n = i + 1;
        trialData[`trial_id_${n}`] = r.trial_id;
        trialData[`trial_in_block_${n}`] = r.trial_in_block;
        trialData[`condition_${n}`] = r.condition;
        trialData[`utterance_${n}`] = r.utterance;
        trialData[`grey_cell_${n}`] = r.grey_cell;
        trialData[`correct_answer_${n}`] = r.correct_answer;
        trialData[`response_${n}`] = r.response;
        trialData[`correct_${n}`] = r.correct;
        trialData[`rt_${n}`] = r.rt;
      });

      this.$magpie.addTrialData(trialData);
      this.$magpie.nextScreen();
    }
  }
};
</script>

<style scoped>
.block-row {
  display: flex;
  gap: 18px;
  justify-content: center;
  align-items: flex-start;
  width: 100%;
}

.trial-slot {
  width: 260px;
}

.trial-slot.hidden {
  visibility: hidden;
}

.utterance {
  text-align: center;
  font-size: 20px;
  min-height: 45px;
  margin-bottom: 8px;
}

.grid-wrapper {
  position: relative;
  width: 260px;
  line-height: 0;
}

.stimulus {
  width: 100%;
  display: block;
}

.cell {
  position: absolute;
  background: transparent;
  border: none;
  padding: 0;
  margin: 0;
  appearance: none;
  -webkit-appearance: none;
  opacity: 0;
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

.selection-marker {
  position: absolute;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: black;
  transform: translate(-50%, -50%);
  pointer-events: none;
}

.selection-marker.topLeft {
  top: 25%;
  left: 25%;
}

.selection-marker.topRight {
  top: 25%;
  left: 75%;
}

.selection-marker.bottomLeft {
  top: 75%;
  left: 25%;
}

.selection-marker.bottomRight {
  top: 75%;
  left: 75%;
}
</style>