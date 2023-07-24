<template>
  <form @submit.prevent="handleSubmit">
    <div class="row1">
      <label>Cardholder Name</label>
      <input
        :class="{ errorcont: cardNameError }"
        type="text"
        placeholder="e.g. Jane Appleseed"
        v-model="liveData.cardName"
        required
      />
      <p ref="error" class="error" v-if="cardNameError">{{ cardNameError }}</p>
    </div>
    <div class="row2">
      <label>Card Number</label>
      <input
        :class="{ errorcont: cardNumberError }"
        type="text"
        placeholder="e.g. 1234 5678 9123 0000"
        v-model="liveData.cardNumber"
        maxlength="16"
        required
      />
      <p ref="error" class="error" v-if="cardNumberError">
        {{ cardNumberError }}
      </p>
    </div>
    <div class="row3">
      <div class="expiry-date">
        <label>Exp. date (mm/yy)</label>
        <div>
          <input
            :class="{ errorcont: cardExpiryError }"
            type="text"
            placeholder="MM"
            v-model="liveData.cardMonth"
            maxlength="2"
            required
  
          />
          <input
            :class="{ errorcont: cardExpiryError }"
            type="text"
            placeholder="YY"
            v-model="liveData.cardYear"
            maxlength="2"
            required
  
          />
        </div>
        <p ref="error" class="error" v-if="cardExpiryError">
          {{ cardExpiryError }}
        </p>
      </div>
      <div class="cvc">
        <label>CVC</label>
        <input
          :class="{ errorcont: cardCVCError }"
          type="text"
          placeholder="e.g. 123"
          maxlength="3"
          v-model="liveData.cardCVC"
          required

        />
        <p ref="error" class="error" v-if="cardCVCError">{{ cardCVCError }}</p>
      </div>
    </div>
    <button @click="handleSubmit">Submit</button>
  </form>
</template>

<script>
export default {
  props: ['liveData'],
  data() {
    return {
      user: {
        cardName: "",
        cardNumber: "",
        cardMonth: "",
        cardYear: "",
        cardCVC: "",
      },
      cardNameError: "",
      cardNumberError: "",
      cardExpiryError: "",
      cardCVCError: "",
      userData : {
        userName: '',
        userNumber: '',
        userExpiry: '',
        userCVC: '',
      }
      
    };
  },
  methods: {

    handleSubmit() {
      this.nameErr();
      this.numberErr();
      this.expiryErr();
      this.cvcErr();
        if ((!this.nameErr() && !this.numberErr() && !this.expiryErr() && !this.cvcErr())) {
            this.userData.userName = this.liveData.cardName;
            this.userData.userNumber = this.liveData.cardNumber;
            this.userData.userExpiry = `${this.liveData.cardMonth}/${this.liveData.cardYear}`;
            this.userData.userCVC = this.liveData.cardCVC;
            this.$emit('returnUserData', this.userData)
        }

    },
    nameErr() {
      const reg = /^[a-zA-z][a-zA-z\s]*$/;
      if (!reg.test(this.liveData.cardName)) {
        this.cardNameError = "Can not contain special characters";
        return true;
      } else {
        this.cardNameError = "";
        return false;
      }
    },
    numberErr() {
      const reg = /^(\d{16})$/;
      if (this.liveData.cardNumber.length <= 0) {
        this.cardNumberError = "Field must not be empty.";
        return true;
      } else if (!reg.test(this.liveData.cardNumber)) {
        this.cardNumberError = "Invalid number";
        return true;
      } else {
        this.cardNumberError = "";
        return false;
      }
    },
    expiryErr() {
      const currentMonth = Number((new Date().getMonth() + 1).toString());
      const currentYear = Number(
        new Date().getFullYear().toString().substring(2)
      );

      if (this.liveData.cardMonth.length <= 0 || this.liveData.cardYear.length <= 0) {
        this.cardExpiryError = "Field must not be empty.";
        return true;
      } else if (Number(this.liveData.cardYear) < currentYear) {
        this.cardExpiryError = "Invalid Year";
        return true;
      } else if (
        Number(this.liveData.cardYear) == currentYear &&
        Number(this.liveData.cardMonth) < currentMonth
      ) {
        this.cardExpiryError = "Invalid Month";
        return true;
      } else {
        this.cardExpiryError = "";
        return false;
      }
    },
    cvcErr() {
      const reg = /^(\d{3})$/;
      if (!reg.test(this.liveData.cardCVC)) {
        this.cardCVCError = "Invalid CVC";
        return true;

      } else {
        this.cardCVCError = "";
        return false
    }
    },
  },
};
</script>

<style>
form {
  display: flex;
  flex-direction: column;
  gap: 1em;
}
form label {
  display: block;
  margin-bottom: .2em;
  text-transform: uppercase;
  font-size: var(--fs-300);
  letter-spacing: 0.15em;
  color: var(--clr-neutral-200);
}
form input {
  width: 100%;
  font-size: var(--fs-550);
}
.row3 {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.expiry-date div {
  display: flex;
  gap: 0.3em;
}
.expiry-date div input {
  width: 45%;
}
form button {
  margin-top: 2em;
}
</style>
