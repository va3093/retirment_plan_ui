<template>
  <div id="app" class="background-color--grey-20">
    <RetirementPlan msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import RetirementPlan from "./pages/RetirementPlan.vue";

export default {
  name: "app",
  components: {
    RetirementPlan
  }
};
</script>

<style lang="scss">
@import "~meos_design/dist/meos_design.css";
@import "~meos_design/src/styles/constants.scss";
@import "~meos_design/src/styles/colors.scss";
@import "~meos_design/src/styles/layout.scss";
#app {
  min-height: 100vh;
}
</style>
