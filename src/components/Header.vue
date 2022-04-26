<template>
  <div class="header-view">
    <h1>{{title}}</h1>
    <p>{{sub}}</p>
  </div>
</template>

<script>
export default {
  name:'Header',
    props:{title:String, sub:String},
};
</script>

<style  scoped>
.header-view{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 416px;
    height: 130px;
}
 .header-view h1 {
  width: 200px;
  height: 70px;
  text-align: center;
  font-size: 30px;
  font-style: normal;
  line-height: 30px;
  padding: 5px;
  font-family: "Source Sans Pro", sans-serif;
  font-weight: 700;
  margin: 24px 0px 16px 0px;

}

 .header-view p {
  text-align: center;
  font-family: "Source Sans Pro", sans-serif;
  font-size: 12px;
  font-style: normal;
  line-height: 15px;
  font-weight: 500;
  color: rgba(34, 34, 34, 0.6);
  margin: 0px;
}
</style>