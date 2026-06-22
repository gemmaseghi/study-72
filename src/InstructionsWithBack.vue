<template>
  <Screen>
    <div class="instructions">
      <h2>{{ pages[page].title }}</h2>

      <div v-html="pages[page].text"></div>

      <div class="button-container">
        <button v-if="page > 0" @click="page--">
          Back
        </button>

        <button v-if="page < pages.length - 1" @click="page++">
          Next
        </button>

        <button v-else @click="$magpie.nextScreen()">
          Continue
        </button>
      </div>
    </div>
  </Screen>
</template>

<script>
export default {
  name: "InstructionsWithBack",
  data() {
    return {
      page: 0,
      pages: [
        {
          title: "Consent form",
          text: `Thank you for your interest in our study. Please read the following information before deciding whether to participate. Your participation is entirely voluntary.
          <br><br>
          Your data will be stored under a randomly assigned participant ID and will therefore be fully anonymized. The data will be stored on a server at the University of Tübingen. 
          <br><br>
          All individuals with access to the data are required to maintain confidentiality. If the results of this study are published, they will be reported only in anonymized form, and it will not be possible to identify you from the published data.
          <br><br>
          You will receive £1.05 for your participation. Please note that compensation can only be provided if you complete the study. If you experience any technical issues, please contact us via Prolific.
          <br><br>
          By continuing to the next screen, you confirm that you have read this information and agree to participate in the study.`
        },
        {
          title: "Welcome",
          text: `Welcome to the experiment! You will first read a set of instructions. The instructions are divided into three parts. Please move to the next screen to read the first part.`
        },
        {
          title: "Instructions",
          text: `In this experiment, you will play a game with another participant. You will play the role of the listener, while the other participant will play the role of the speaker. 
          <br><br>
          Each screen contains five grids, each with four objects and a description above it. At the start of each screen, only the leftmost grid will be visible. Select the object indicated by the description above the grid. Each correct selection will reveal the next grid to the right. After all five grids have been revealed, you will proceed to the next screen.
          <br><br>
          The description is produced by the speaker to indicate one of the objects in the grid. You will only be presented the speaker's description in written form, you won't hear it spoken aloud.`
        },
        {
          title: "Instructions",
          text: `The speaker sees a slightly different version of the grids. Their grids contain only three objects because one cell is hidden by an occluder. In your grid, the speaker's occluded cell is shown as a grey cell. This means that the speaker cannot see the object in the grey cell. 
          <br><br>
          If the grey cell changes position between screens, this means that a different cell is occluded from the speaker's view.
          <br><br>
          Apart from the hidden object, both grids contain the same objects. However, the position of the visible objects is shuffled across the two grids, so the speaker cannot use location words (e.g., "top left" or "bottom right") to refer to an object.`
        },
        {
          title: "Instructions",
          text: `On the speaker's screen, one of the visible objects is marked with an asterisk (*). Their task is to describe that object. 
          <br><br>
          Your task is to use their description, which will appear above the grid, to determine which object they intended to refer to and select it.
          <br><br>
          At the end of the experiment, you will be asked to complete a short questionnaire.`
        },
        {
          title: "Example",
          text: `<img src="instructions/example_view.png" style="width: 800px; max-width: 100%;" />
          <p>
            Example of the speaker's view (left) and your view (right).
            The grey cell indicates the object that is hidden from the speaker.
            The asterisk (*) marks the object that the speaker has to describe.
          </p>
          <p>
            During the experiment, you will only see the right view. The speaker's view is shown here only to illustrate how the game works.
            Your task is to click on the object that you think the speaker is referring to.
          </p>`
        }
      ]
    };
  }
};
</script>

<style scoped>
.instructions {
  width: 600px;
  margin: 0 auto;
  text-align: justify;
}

.instructions h2 {
  text-align: center;
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 30px;
}

.button-container button {
  width: auto;
  margin: 0 5px;
}
</style>