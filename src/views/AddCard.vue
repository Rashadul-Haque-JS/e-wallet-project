<template>
  <div class="add-card">
    <Header :title="title" :sub="subtitle" />
    <CardPreView :user="user"   />
    <Form @save="passData" :user="user" :btnText="btnText"  :lists="lists" />
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import CardPreView from "../components/CardPreView.vue";
import Form from "../components/Form.vue";


export default {
  name:'AddCard',
  props: { user: Object, lists:Array, headline:Object, btnText:String },
  data() {
    return {
      title: this.headline.title,
      subtitle: this.headline.sub,
      miscs:this.misc,
    };
  },
  components: { Form,  Header, CardPreView },

  methods: {
    passData() {
      this.$emit("store", { ...this.user });
    },
    
  },
};
</script>

<style  scoped>
.add-card {
  width: 416px;
  height: 896px;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-shadow: -3px 4px 33px 18px rgba(0, 0, 0, 0.1);
  border-radius: 32px;
  
}
</style>
