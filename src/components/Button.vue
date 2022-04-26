<template>
  <div>
    <button type="submit" class="btn" @click="addCard">{{texts}}</button>
  </div>
</template>

<script>
export default {
  name: "Button",
  props:{texts:String},
  
  methods: {
    addCard() {
      this.$emit("send");
    },
  },
};
</script>

<style scoped>
.btn {
  width: 382px;
  height: 56px;
  margin-top: 42px;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.btn:hover {
  background-color: #000;
  color: #fff;
}
</style>