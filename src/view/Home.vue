<template>
  <nav-bar />
  <calc-option/>
  <!-- <calculation-section/> -->
</template>

<script>
import NavBar from "../components/NavBar.vue";
// import CalculationSection from '../components/CalculationSection.vue'
import CalcOption from '../components/CalcOption.vue'


export default {
  name: "Home",
  components: {
    NavBar,
    CalcOption
    // CalculationSection,
  },
};
</script>
