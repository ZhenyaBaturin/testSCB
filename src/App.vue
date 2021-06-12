<template>
  <StepThree msg="Шаг 3 - Паспорт" />
</template>

<script>
import StepThree from "./components/StepThree.vue";

export default {
  name: "App",
  data: function () {
    return {};
  },
  components: { StepThree },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
