<template>
  <!-- <div class="modal-backdrop"> -->
    <div class="modal-content">
        <img src="../assets/images/icon-complete.svg" alt="" srcset="">
            <div class="success-text">
              <h1>Thank you!</h1>
              <p>We've added your card details</p>
            </div>
            <button id="btn-continue" class="i-100w" @click="close">Continue</button>
    </div>
  <!-- </div> -->
</template>

<script>
export default {
    methods: {
        close() {
            this.$emit("closeModal", true)
        }
    }
}
</script>

<style>
.modal-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  line-height: 1.2;
  gap: 2em;
}
.modal-content img {
  width: 3.5rem;
}
.modal-content h1 {
  text-transform: uppercase;
  color: var(--clr-neutral-10);
  font-size: 3rem;
}
.modal-content p {
  color: var(--clr-neutral-50);
  font-size: 1rem;
}
.modal-content button {
    width: 100%;
}
</style>