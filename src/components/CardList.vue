<template>
  <div class="card-box">
    <CardPreView class="card-list"
      v-for="(obj, index) in cardLists"
      :key="index"
      :user="obj"
      :index="index"
      :obj="obj"
      @click.native="cardActive(obj)"
    />
  </div>
</template>

<script>
import CardPreView from "./CardPreView.vue";
export default {
  name: "CardList",
  props: { cardLists: Array },
  components: { CardPreView },

  methods: {
    cardActive(obj) {
      this.$emit("choose", obj);
    },
  },
};
</script>

<style  scoped>
.card-box {
  display: grid;
  grid-auto-rows: 50px;
}

.card-list:hover{
  transform: translateY(-10px);
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
  z-index: 1;
}
</style>