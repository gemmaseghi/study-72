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
          title: "Consent Form",
          text: `
            <p>
              Thank you for your interest in our study. Please read the following information before deciding whether to participate. Your participation is entirely voluntary.
            </p>

            <p>
              Your data will be stored under a randomly assigned participant ID and will therefore be fully anonymized. The data will be stored on a server at the University of Tübingen.
            </p>

            <p>
              All individuals with access to the data are required to maintain confidentiality. If the results of this study are published, they will be reported only in anonymized form, and it will not be possible to identify you from the published data.
            </p>

            <p>
              You will receive £1.40 for your participation. Please note that compensation can only be provided if you complete the study. If you experience any technical issues, please contact us via Prolific.
            </p>

            <p>
              By continuing to the next screen, you confirm that you have read this information and agree to participate in the study.
            </p>
          `
        },
        {
          title: "Welcome",
          text: `
            <p>
              Welcome to the experiment! You will first read a set of instructions. It is important that you read them carefully. The instructions are divided into three parts. Please move to the next screen to read the first part.
            </p>
          `
        },
        {
          title: "Instructions",
          text: `
            <p>
              In this experiment, you will play a coordination game with a virtual speaker named <strong>Sam</strong>.

              Sam will choose one object among the four contained in a grid and describe it.
            </p>

            <p>
              <strong>Sam's description will appear above the grid</strong>. You will only see the description in written form, you won't hear it spoken aloud.
            </p>

            <p>For example:</p>

            <div class="instruction-figure">
              <p class="image-caption">
                The turtle
              </p>

              <img
                src="instructions/instruction_01.png"
                class="instruction-image"
              />
            </div>

            <p>
              <strong>Your task will be to select the object described by Sam by clicking on it</strong>. 
            </p>
          `
        },
        {
          title: "Instructions",
          text: `
            <p>
              But Sam has a <strong>blind spot</strong>! You will always see four objects, but Sam only sees three. This is because <strong>one of Sam's cells is hidden by an occluder</strong>. But <strong>Sam doesn't know that he has a blindspot</strong>. He thinks that you see the same three objects and not the fourth one.
            </p>

            <p>
              In your grid, Sam's occluded cell is shown as a grey cell. This means that <strong>Sam cannot see the object in the grey cell</strong>.
            </p>

            <p>
              Apart from the hidden object, your grid and Sam's one contain the same objects. However, the position of the visible objects is shuffled across them, so Sam cannot use location words (e.g., "top left" or "bottom right") to refer to an object.
            </p>

            <p>
              On Sam's screen, one of the visible objects is marked with an asterisk (*). His task is to describe that object.
            </p>

            <p>Sam's view is on the left and your view is on the right:</p>

            <img
              src="instructions/example_view.png"
              class="example-image"
            />
          `
        },
        {
          title: "Instructions",
          text: `
            <p>
              In this task, each screen contains <strong>five grids</strong>. At the beginning of each screen, <strong>one large grid will be shown in the centre of the page</strong>. This is the only grid in which you need to select an object.
            </p>

            <p>
              Read the description above the large grid and click on the object that you think Sam is referring to. <strong>After each selection, the completed grid will move to the top of the screen, where it will appear smaller and your selection will remain marked with a black dot.</strong> At the same time, the next grid will immediately appear in the large display in the centre of the page. <strong>The grids shown at the top are only there as a record of your previous selections, you do not need to click on them again.</strong>
            </p>

            <p>
              Once you have selected an object in all five grids, <strong>the selection grid in the centre of the screen will be replaced by a square with "Next" written in it</strong>. Click on it to proceed to the next screen.
            </p>

            <p>
              <strong>Within a screen, the grey cell always remains in the same position. Across screens, the grey cell may move to a different position.</strong> When this happens, it means that a different cell is hidden from Sam's view.
            </p>

            <p>
              At the end of the experiment, you will be asked to complete a short questionnaire.
            </p>
          `
        }
      ]
    };
  }
};
</script>

<style>
.instructions {
  width: 700px;
  max-width: 95vw;
  margin: 0 auto;
  text-align: justify;
}

.instructions h2 {
  text-align: center;
}

.instructions p {
  font-size: 18px;
  line-height: 1.6;
  margin-bottom: 12px;
}


.example-image {
  display: block;
  margin: 24px auto;
  max-width: 650px;
  width: 100%;
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

.instruction-figure {
  text-align: center;
  margin: 8px 0;
}

.image-caption {
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
}

.instruction-image {
  display: block;
  margin: 0 auto;
  max-width: 300px;
  width: auto;
  height: auto;
}

.example-image {
  display: block;
  margin: 24px auto;
  max-width: 650px;
  width: auto;
  height: auto;
}
</style>