<template>
  <nav-bar />
  <calculation-section/>
</template>

<script>
import NavBar from "../components/NavBar.vue";
import CalculationSection from '../components/CalculationSection.vue'


export default {
  name: "Home",
  components: {
    NavBar,
    CalculationSection,
  },
};
</script>
