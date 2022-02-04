<template>
  <div class="button-component">
    <button @click="buttonClick" class="button">Hava Durumu Ara</button>
  </div>
</template>
<script>
export default {
  name: "Button",
  props: {
    buttonClick: {
      type: Function,
    },
  },
};
</script>

<style scoped>
.button-component {
  text-align: center;
}
.button {
  width: 250px;
  height: 35px;
  margin: 20px 0;
  background: #006fd6;
  border-radius: 40px;
  border: none;
  color: white;
  font-family: Poppins;
  font-weight: bold;
  font-size: 14px;
  line-height: 24px;
  cursor: pointer;
}
</style>
