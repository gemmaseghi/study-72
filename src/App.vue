<template>
  <Experiment title="Perspective-taking experiment">

    <InstructionsWithBack />

    <PracticeBlock :practiceTrials="practiceTrials" />

    <GridTrial
      v-for="block in trialBlocks"
      :key="block[0].block_id"
      :block="block"
    />

    <Questionnaire />

    <SubmitResultsScreen />
  </Experiment>
</template>

<script>
import trialBlocks from "./trials";
import InstructionsWithBack from "./InstructionsWithBack.vue";
import PracticeBlock from "./PracticeBlock.vue";
import practiceTrials from "./PracticeTrials";
import GridTrial from "./GridTrial.vue";
import Questionnaire from "./Questionnaire.vue";

export default {
  name: "App",
  components: {
    InstructionsWithBack,
    GridTrial,
    PracticeBlock,
    Questionnaire
  },
  data() {
    return {
      trialBlocks,
      practiceTrials
    };
  }
};
</script>

<style>
.experiment {
  width: 1500px !important;
  max-width: 95vw !important;
}
</style>