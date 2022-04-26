<template>
  <div class="card-demo" :class="user.vendor">
    <img class="wifi" :src="wifiIcon" alt="wifi" />
    <img class="chip" :class="chipIcon" :src="chip" alt="chip" />
    <!-- <img class="delete-card" src="../assets/delete.svg" alt="" @click="removeCard" /> -->
    <span v-if="user.vendor == ''">
      <img class="logo" :src="logo" alt="logo"
    /></span>
    <span v-else>
      <img
        class="logo"
        :src="require(`../assets/${user.vendor}.svg`)"
        alt="logo"
      />
    </span>

    <p class="card-number">{{ numberSpace }}</p>

    <p class="label-name">CARDHOLDER NAME</p>
    <p class="name">{{ user.cardHolder }}</p>

    <p class="label-date">VALID THRU</p>
    <div class="card-validity-date">
      <p>{{ user.expireMonth }}</p>
      <p>/</p>
      <p>{{ user.expireYear }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardPreView",
  props: { user: Object },

  computed: {
    numberSpace() {
      let num;
      if (this.user.cardNumber) {
        num = this.user.cardNumber
          .replace(/\W/gi, "")
          .replace(/(.{4})/g, "$1 ");
      }
      return num;
    },

    wifiIcon() {
      if (
        this.user.vendor == "ninja" ||
        this.user.vendor == "blockchain" ||
        this.user.vendor == "evil"
      )
        return require("../assets/wifi_white.svg");
      return require("../assets/wifi.svg");
    },

    chipIcon() {
      if (this.user.vendor != "") return "icon-white";
      return "";
    },
  },

  data() {
    return {
      chip: require("../assets/chip.svg"),
      logo: require("../assets/bitcoin.svg"),
    };
  },

 
};
</script>

<style  scoped>
.card-demo {
  width: 342px;
  height: 200px;
  position: relative;
  border-radius: 8px;
  background-color: #d0d0d0;
  margin: 8px 0px 42px 0px;
  padding: 12px 20px;
  cursor: pointer;
  text-shadow: -2px -1px 1px rgb(14, 13, 13), 1px 1px 1px rgb(248, 244, 244),
    1px 0px 1px rgba(255, 255, 255, 1), -1px -1px 1px rgb(22, 21, 21),
    -1px 1px 1px rgb(240, 233, 233);
  -webkit-text-stroke: 1px rgba(0, 0, 0, 0.2);
  -webkit-text-stroke: 1px rgba(0, 0, 0, 0.2);
}

/* .card-demo:hover {
} */

.card-number,
.logo,
.wifi,
.chip,
.label-name,
.name,
.label-date,
.card-validity-date,
.delete-card {
  position: absolute;
  font-family: "PT Mono", monospace;
}

.wifi {
  width: 44px;
  height: 44px;
  left: 24px;
  top: 16px;
}

.chip {
  width: 50px;
  height: 40px;
  left: 20px;
  top: 56px;
}

.logo {
  right: 8px;
  top: 24px;

  width: 56px;
}

.card-number {
  width: 350px;
  height: 42px;
  top: 80px;
  left: 16px;
  text-align: center;
  font-size: 28px;
}

.label-name {
  left: 16px;
  bottom: 40px;
  font-size: 12px;
  line-height: 13px;
  letter-spacing: 0.1rem;
}

.name {
  left: 16px;
  bottom: 12px;
  font-size: 16px;
  font-weight: normal;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
}

.label-date {
  right: 16px;
  bottom: 40px;
  font-size: 12px;
  line-height: 13.5px;
}
.card-validity-date {
  display: flex;
  justify-content: center;
  align-items: center;
  right: 16px;
  bottom: 12px;
  width: 72px;
  margin: 0px;
  padding: 0px;
}

.card-validity-date p {
  font-size: 16px;
  font-weight: normal;
  text-align: center;
  letter-spacing: .1rem;
}

.bitcoin {
  background-color: #ffae34;
  color: #222222;
}

.blockchain {
  background-color: #8b58f9;
  color: #ffffff;
}

.ninja {
  background-color: #222222;
  color: #ffffff;
}

.evil {
  background-color: #f33355;
  color: #ffffff;
}

.icon-white {
  background-color: #ffffff;
  border-radius: 8px;
}
</style>