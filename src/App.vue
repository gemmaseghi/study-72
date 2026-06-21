<template>
  <Experiment title="Perspective-taking experiment">

    <InstructionsWithBack />

    <PracticeBlock :practiceTrials="practiceTrials" />

    <GridTrial
      v-for="trial in trials"
      :key="trial.id"
      :trial="trial"
    />

    <Questionnaire />

    <SubmitResultsScreen />
  </Experiment>
</template>

<script>
import _ from "lodash";
import trials from "./trials";
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
      trials,
      practiceTrials
    };
  },
  computed: {
    _() {
      return _;
    }
  }
};
</script>