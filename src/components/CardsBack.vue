<template>
  <div class="card-back-wrapper" :class="users.vendor">
    <div class="card-back-top">
      <img
        class="back-and-delete"
        src="../assets/go_back.svg"
        alt="back space"
        @click="flipOff"
      />

      <img
        class="back-and-delete"
        src="../assets/delete.svg"
        alt="delete icon"
        @click="removeActCard"
      />
    </div>

    <div class="rabon-dark"></div>
    <p class="ccv-label">CVC</p>
    <div class="ccv-number-container">
      <div>
        <p class="strip"></p>
        <p class="strip"></p>
        <p class="strip"></p>
      </div>
      <span class="four-digits">{{ cardNumLastFourDgts }}</span
      ><span class="cvc-num">{{ cvc }}</span>
    </div>
    <p class="others-info">
      This card is Lorem ipsum dolor sit amet consectetur adipisicing elit.
      Totam inventore ad earum
      <span class="last-line"
        >possimus? Distinctio officiis: +46 016 1234567
      </span>
    </p>
  </div>
</template>

<script>
export default {
  props: { user: Array, cvc:Number },
  data() {
    return {
      users: this.user[this.user.length - 1],
    };
  },

  computed: {
    cardNumLastFourDgts() {
      return this.users.cardNumber.substr(-4);
    },
  },

  methods: {
    flipOff() {
      this.$emit("flipFront");
    },

    removeActCard() {
      this.$emit("del");
    },
  },
};
</script>

<style scoped>
/* CSS FOR BACK PAGE */

.card-back-wrapper {
  width: 382px;
  height: 200px;
  position: relative;
  border-radius: 8px;
  margin: 8px 0px 42px 0px;

  padding: 12px 0px;
}

.rabon-dark {
  height: 40px;
  background-color: #2e1503;
}

.ccv-label {
  height: 20px;
  margin: 10px 20px -5px 0px;
  text-align: end;
  font-size: 10px;
  color: #fff;
}

.ccv-number-container {
  height: 40px;
  background-color: #fff;
  width: 92%;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 4px;
}
.ccv-number-container div {
  background-color: #f2efbd;
  width: 320px;
  margin-left: 0px;
}

.ccv-number-container div .strip {
  width: 318px;
  height: 1px;
  border-top: solid 1px #f29f05;
  margin: 7px 0px 8px 2px;
}

.ccv-number-container .cvc-num {
  margin-right: 8px;
  font-weight: bold;
  transform: translateX(-32px);
}

.ccv-number-container .four-digits {
  transform: translateX(-40px);
}

.others-info {
  font-size: 0.8rem;
  line-height: 14px;
  margin: 6px 10px;
  padding: 10px;
  opacity: 0.8;
  color: #fff;
  font-weight: bold;
}

.last-line {
  display: block;
}

.card-back-top {
  display: flex;
  justify-content: space-between;

  padding: 0px 8px;
  transform: translateY(-8px);
}

.back-and-delete {
  width: 16px;
  background-color: #fffce6;
  /* margin-top: -3px; */
  cursor: pointer;
}
.bitcoin {
  background-color: #ffae34;
  color: #222222;
}

.blockchain {
  background-color: #8b58f9;
}

.ninja {
  background-color: #222222;
}

.evil {
  background-color: #f33355;
}
</style>