<template>
  <nav-bar />
  <calc-option/>
  <computed-test/>
  <!-- <calculation-section/> -->
</template>

<script>
import NavBar from "../components/NavBar.vue";
// import CalculationSection from '../components/CalculationSection.vue'
import CalcOption from '../components/CalcOption.vue'
import ComputedTest from '../components/ComputedTest.vue';


export default {
  name: "Home",
  components: {
    NavBar,
    CalcOption,
    ComputedTest
    // CalculationSection,
  },
};
</script>
