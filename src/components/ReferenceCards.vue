<template>
  <div class="ref-card ref-card__front">
    <img
      class="card_img"
      src="../assets/images/bg-card-front.png"
      alt="card front"
      srcset=""
    />
    <img
      class="card_logo"
      src="../assets/images/card-logo.svg"
      alt="card logo"
      srcset=""
    />
    <p id="ref-card-number" class="card_number">{{ liveData.cardNumber }}</p>
    <p id="ref-card-name" class="card_name">{{ liveData.cardName }}</p>
    <div id="ref-card-exp" class="card_exp">
      <span id="ref-card-exp-month">{{ liveData.cardMonth }}</span>
      <span>/</span>
      <span id="ref-card-exp-year">{{ liveData.cardYear }}</span>
    </div>
  </div>
  <div class="ref-card ref-card__back">
    <img
      class="card_img"
      src="../assets/images/bg-card-back.png"
      alt="card back"
      srcset=""
    />
    <p id="ref-card-cvc" class="card_cvc" aria-placeholder="CVC">{{ liveData.cardCVC }}</p>
  </div>
</template>

<script>
export default {
    // props: ["liveData"],
    props: {
        liveData: {
            type: Object,
            default: {},
            cardName :{
                type: Number,
                default: "John Doe",
                required: true,
            }
        }
    }
}

</script>

<style>

.ref-card {
  --card-padding: 1.5rem;

  position: relative;
  width: min-content;
  color: var(--clr-neutral-80);

  text-transform: uppercase;
  box-shadow: var(--boxshadow-1);
  border-radius: var(--border-radius-card);
}

.ref-card img {
  max-width: revert;
}
.ref-card > *:not(.card_img) {
  position: absolute;
}
.ref-card__front {
  /* border: 5px solid red; */
  top: -5%;
}
.ref-card__back {
  /* border: 5px solid green; */
  margin-left: auto;
}
.card_logo {
  top: var(--card-padding);
  left: var(--card-padding);
}
.card_name {
  bottom: var(--card-padding);
  left: var(--card-padding);
}
.card_exp {
  bottom: var(--card-padding);
  right: var(--card-padding);
}
.card_number {
  top: 50%;
  left: var(--card-padding);
  font-size: var(--fs-600);
  color: var(--clr-neutral-100);
}
.card_cvc {
  top: 45.5%;
  right: 12%;
}
.card_name,
  .card_exp,
  .card_cvc {
    font-size: var(--fs-500);
  }

@media (prefers-color-scheme: dark) {
  .ref-card {
    color: var(--clr-neutral-10);
  }
  .card_number {
    color: var(--clr-neutral-10);
  }
}

@media (max-width: 915px) {
  .main_aside {
    grid-column: 1/2;
    position: relative;
  }
  .ref-card {
    --card-padding: 1rem;
  }
  .card_name,
  .card_exp,
  .card_cvc {
    font-size: var(--fs-400);
  }
  .ref-card__front {
    position: absolute;
    z-index: 2;
    top: 60%;
    left: -5%;
  }
  .ref-card__back {
    position: absolute;
    top: 20%;
    right: -5%;
  }
  .card_img {
    width: 15em;
  }
  .card_number {
    font-size: var(--fs-500);
  }
  .card_logo {
    width: 32px;
  }
  .card_cvc {
  top: 44.5%;
}
}
</style>
