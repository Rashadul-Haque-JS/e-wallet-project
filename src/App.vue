<template>
  <div id="app">
    <Home
      @chooseCard="getActiveCard"
      @toggle="toggleViewAdd"
      @showIcon="iconDisplay"
      @toBack="flipActBack"
      @toFront="flipActFront"
      @delete="removeActiveCard"
      :headline="headlines.home"
      :btnText="btnText.homeName"
      :cardLists="cardLists"
      :activeCard="activeCard"
      :user="user"
      :flip="isFlip"
      :isIcon="isIcon"
      :cvc="cvcNum"
      v-if="isView"
    />
    <AddCard
      @store="getData"
      :user="user"
      :lists="cardLists"
      :headline="headlines.addCard"
      :btnText="btnText.addName"
      v-else
    />
  </div>
</template>

<script>
import Home from "./views/Home.vue";
import AddCard from "./views/AddCard.vue";

export default {
  name: "app",
  data() {
    return {
      isView: true,
      isFlip: true,
      isIcon: false,

      // Generate CVC number
      cvcNum: null,

      // Data storage for creating cardlists
      cardLists: [],
      // Data storage for creating Active card
      activeCard: [],

      // Data init state
      user: {
        cardNumber: null,
        cardHolder: "",
        expireMonth: 'MM',
        expireYear: 'YY',
        CCV: null,
        vendor: "",
      },

      // Data for header sections
      headlines: {
        home: { title: "E-WALLET", sub: "ACTIVE CARD" },
        addCard: { title: "ADD A NEW BANK CARD", sub: "NEW CARD" },
      },
      //Data for buttons inner text
      btnText: { addName: "ADD CARD", homeName: "ADD A NEW CARD" },
    };
  },

  created() {
    if (localStorage.getItem("cardList") != undefined) {
      this.cardLists = JSON.parse(localStorage.getItem("cardList"));
    }

    if (localStorage.getItem("card") != undefined) {
      this.activeCard.push(JSON.parse(localStorage.getItem("card")));
    }
  },

  components: {
    AddCard,
    Home,
  },

  methods: {
    getData(data) {
      (this.isView = true), this.cardLists.push(data);
      localStorage.setItem("cardList", JSON.stringify(this.cardLists));
    },

    getActiveCard(obj) {
      this.activeCard.push(obj);
      localStorage.setItem("card", JSON.stringify(obj));
      this.isFlip = true;
      this.cvcNum = Math.floor(Math.random() * (999 - 100 + 1) + 100);
    },

    toggleViewAdd() {
      this.isView = false;
    },
    iconDisplay() {
      this.isIcon = true;
    },
    

    flipActBack() {
      this.isFlip = false;
      this.isIcon = false;
    },

    flipActFront() {
      this.isFlip = true;
      this.isIcon = false;
    },
    removeActiveCard() {
      this.isFlip = true;
      this.activeCard.pop();
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=PT+Mono&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:wght@200;300;400;600;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  display: flex;
  justify-content: space-around;
  margin-top: 30px;
  
}
</style>