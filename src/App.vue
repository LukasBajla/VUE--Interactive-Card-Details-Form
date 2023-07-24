<template>
  <main>
    <div class="main-grid">
      <div class="main_aside">
        <ReferenceCards
        :liveData="liveData" />
      </div>
      <div class="main_input">
        <div class="project-info">
          <h1>Project: <span>Interactive Card Details Form</span></h1>
          <p>Please input valid credit card data into the required fields.
Input data is updated live in the credit card mockup on the side or top of the page.
After you input a valid data, pressing the 'Confirm' button will show another screen confirming the correct input.</p>
        </div>
        <CardDetailsForm
          @returnUserData="getUserData"
          v-if="!userInputComplete"
          :liveData="liveData"
        />
        <ModalUserInput @closeModal="closeModal" v-if="userInputComplete" />
      </div>
    </div>
  </main>
  <div class="attribution">
            Challenge by
            <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
              >Frontend Mentor</a
            >. Coded by <a target="_blank" href="https://github.com/LukasBajla">Lukas Bajla</a>.
          </div>
</template>

<script>
import CardDetailsForm from "./components/CardDetailsForm.vue";
import ModalUserInput from "./components/ModalUserInput.vue";
import ReferenceCards from "./components/ReferenceCards.vue";

export default {
  name: "App",
  components: { CardDetailsForm, ModalUserInput, ReferenceCards },
  data() {
    return {
      liveData: {
        cardName: "",
        cardNumber: "",
        cardMonth: "",
        cardYear: "",
        cardCVC: "",
      },
      userData: null,
      userInputComplete: false,

    };
  },
  methods: {
    getUserData(data) {
      this.userData = data;
      this.liveData = {
        cardName: "",
        cardNumber: "",
        cardMonth: "",
        cardYear: "",
        cardCVC: "",
      },
      this.userInputComplete = true;
    },
    closeModal(state) {
      this.userInputComplete = !state;
    },
  },
};
</script>

<style>

.project-info {
  font-size: var(--fs-200);
  color: var(--clr-neutral-300);
  display: grid;
  gap: 1em;
}
.project-info p {
  opacity: .5;
}
.project-info span {
  background: -webkit-linear-gradient(60deg, #6448fe, #600594);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}



main {
  display: flex;
  align-items: center;
  justify-content: center;
}
main::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 40vw;
  min-height: 100dvh;
  background-image: url(./assets/images/bg-main-desktop.png);
  background-size: cover;
}

.main-grid {
  margin: 0 auto;
  display: grid;
  place-content: center;
  gap: 6vw;
  grid-template-columns: 28em 1fr;
  min-height: 100dvh;
  /* border: 5px solid royalblue; */
}

@media (max-width: 915px) {
  .main-grid {
    grid-template-columns: 1fr;
    grid-template-rows: 15em 1fr;
    /* min-height: revert; */
  }
  main::before {
    background-image: url(./assets/images/bg-main-mobile.png);
    width: 100vw;
    min-height: 15em;
  }
}
.main_aside {
  grid-column: 1/2;
  /* border: 5px solid teal; */
}
@media (max-width: 915px) {
  .main_aside {
    grid-column: 1/2;
    position: relative;
  }
}
.main_input {
  grid-column: 2/3;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 2.5em;
  width: min(85vw, 20em);
}
@media (max-width: 915px) {
  .main_input {
    grid-column: 1/2;
    margin: 3em 0;
    justify-content: flex-start;
  }
}
</style>
