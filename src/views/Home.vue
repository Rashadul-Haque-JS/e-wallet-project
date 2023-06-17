<template>
  <div class="home">
    <Header :title="title" :sub="subtitle" />

    <div class="active-card-container">
      <span v-if="toggleNotes">
        Status empty. Choose one from the list bellow.
      </span>
      <img
        class="turn-card"
        src="../assets/flip_view.svg"
        alt="flip icon"
        @click="flipCardsBack"
        v-if="isIcon"
      />
      <CardPreView
        class="cursor-view"
        @mouseover.native="displayIcon"
        :user="activeCard[activeCard.length - 1]"
        :isIcon="isIcon"
        v-if="flip"
      />
      <CardsBack
        @flipFront="flipCardsFront"
        @del="removeCard"
        :user="activeCard"
        :cvc="cvc"
        v-else
      />
    </div>

    <CardList @choose="cardAct" :cardLists="cardLists" :user="user" />

    <div class="btn-area">
      <Button @send="showAddCard" :texts="texts" />
    </div>
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import CardList from "../components/CardList.vue";
import Button from "../components/Button.vue";
import CardPreView from "../components/CardPreView.vue";
import CardsBack from "../components/CardsBack.vue";
export default {
  name: "Home",
  props: {
    headline: Object,
    btnText: String,
    cardLists: Array,
    activeCard: Array,
    user: Object,
    flip: Boolean,
    isIcon: Boolean,
    cvc:Number
  },
  components: { Header, CardList, Button, CardPreView, CardsBack },


  data() {
    return {
      title: this.headline.title,
      subtitle: this.headline.sub,
      texts: this.btnText,
     
    };
  },

  computed: {
    toggleNotes() {
      if (this.activeCard.length < 1) return true;
      return false;
    },
  },

  methods: {
    showAddCard() {
      this.$emit("toggle");
    },
    cardAct(data) {
      this.$emit("chooseCard", data);
    },

    displayIcon() {
      this.$emit("showIcon");
    },

  
    flipCardsBack() {
      this.$emit("toBack");
    },

    flipCardsFront() {
      this.$emit("toFront");
    },
    removeCard() {
      this.$emit("delete");
    },
  },
};
</script>

<style scoped>
.home {
  position: relative;
  width: 416px;
  height: 896px;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: -3px 4px 33px 18px rgba(0, 0, 0, 0.1);
  border-radius: 32px;
  background-color: #FEF17F;
  border: 2px solid rgb(176, 173, 173);
}

.active-card-container {
  position: relative;
  height: 264px;
  cursor: pointer;
  overflow: hidden;
}
.active-card-container span {
  text-align: center;
  width: fit-content;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1rem;
  padding: 120px 12px 0px 32px;
}

.cursor-view {
  cursor: auto;
}

.turn-card {
  position: absolute;
  right: 180px;
  top: 24px;
  font-weight: bolder;
  width: 18px;
  z-index: 1;
}

.btn-area {
  position: absolute;
  width: 382px;
  height: 80px;
  left: 16px;
  top: 780px;
}

.delete-card:hover {
  display: block;
}
</style>