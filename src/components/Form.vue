<template>
  <div>
    <div class="form-container" @submit.prevent="iisSubmitted = true, uniqueNumber">
      <!-- Form formation -->
      <form class="card-formation">
        <div class="card-info">
          <label for="card-number">CARD NUMBER</label>
          <input
            class="form-control"
            id="card-number"
            placeholder="XXXX XXXX XXXX XXXX"
            maxlength="16"
            v-model.trim="users.cardNumber"
            required
          />
          <span class="alerts" v-if="uniqueNumber"
            >Number is already taken, choose new one!</span
          >
        </div>
        <div class="card-info">
          <label for="name">CARDHOLDER NAME</label>
          <input
            type="text"
            class="form-control"
            id="name"
            placeholder="FirstName LastName"
            v-model.trim="users.cardHolder"
            required
          />
        </div>

        <div class="card-validation-info">
          <div class="validation-info-month-year">
            <label for="date">EXP. MONTH</label>
            <select
              class="validity"
              name="month"
              id="months"
              v-model.trim="users.expireMonth"
              required
            >
              <option
                v-for="month in months"
                :key="month"
                :value="month.toString().length < 2 ? '0' + month : month"
              >
                {{ month }}
              </option>
            </select>
          </div>
          <div class="validation-info-month-year">
            <label for="date">EXP. YEAR</label>
            <select
              class="validity"
              name="year"
              id="years"
              v-model.trim="users.expireYear"
              required
            >
              <option
                v-for="year in years"
                :key="year"
                :value="year.toString().substr(2)"
              >
                {{ year }}
              </option>
            </select>
          </div>
        </div>

        <div class="card-info">
          <label for="select-name">VENDOR</label>

          <select class="select-vendor" v-model="users.vendor" required>
            <option value="bitcoin">BITCOIN INC</option>
            <option value="ninja">NINJA BANK</option>
            <option value="blockchain">BLOCK CHAIN INC</option>
            <option value="evil">EVIL CORP</option>
          </select>
        </div>

        <Button @send="saveData" :texts="btnText" />
      </form>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Form",
  props: { user: Object, lists: Array, btnText: String },

  data() {
    return {
      months: 12,
      years: [2022, 2023, 2024, 2025, 2026],
      isSubmitted: false,
      users: this.user,
      fact:false,
    };
  },

  components: { Button },

computed:{
 uniqueNumber() {
    this.lists.forEach((el) => {
      if (el.cardNumber == this.users.cardNumber) {
        this.fact = true;
      } else {
        this.fact = false;
      }
    });
    return this.fact
  },
},
 

  methods: {
    saveData() {
      if (
        this.users.vendor &&
        this.users.cardNumber &&
        this.users.cardHolder &&
        this.users.expireMonth &&
        this.users.expireYear &&
        !this.uniqueNumber
      ) {
        this.$emit("save");
      }
    },
  },
};
</script>

<style scoped>
.form-container {
  padding-bottom: 24px;
}
.form-container,
.card-info {
  width: 382px;

  display: flex;
  flex-direction: column;
}

form input[type="text"] {
  margin-top: 5px;
  font-family: "PT Mono", monospace;
  border: solid 1px #000;
}

.form-control {
  width: 374px;
  height: 50px;
  border-radius: 8px;
}

.card-info {
  margin: 14px 0px;
}

.card-info,
.card-validation-info label {
  font-size: 12px;
  font-family: "PT Mono", monospace;
  font-weight: 400;
  text-align: start;
}
.card-info select {
  margin-top: 5px;
}

.alerts {
  color: #ee1919;
  margin: 3px 0px 0px 0px;
  padding: 0px;
}

.card-validation-info {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-gap: 25px;
}

.card-validation-info select option {
  background-color: #000;
  color: #fff;
  border-radius: 10px;
}
.validation-info-month-year {
  display: block;
}

.validity {
  width: 175px;
  height: 56px;
  border-radius: 8px;
}

.select-vendor {
  width: 374px;
  height: 56px;
  border-radius: 8px;
}

.select-vendor > option {
  width: 368px;
  background-color: #000;
  color: #fff;
  border-radius: 5px;
}
</style>
