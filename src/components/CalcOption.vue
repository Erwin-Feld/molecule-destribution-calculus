<template>
  <section>
    <ul>
      <li
        v-for="item in requestData.molecules"
        :key="item.id"
        @click="toggleClass($event.target)"
      >
        {{ item.name }}
      </li>
    </ul>
  </section>
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";
import axios, { get } from "axios";
import molecules from "../assets/comp.Data/molecules.json";

export default {
  // name: "CalculationSection",

  data() {
    return {
      selectedElements: [],
      requestData: molecules,
    };
  },

  methods: {
    toggleClass(target) {
      target.classList.toggle("selected");
      console.log(this.selectedElements)
      this.selectedElements.push(1)

    },

    async fetchData() {
      try {
        let res = await axios({
          url: process.env.VUE_APP_ENV_DB_TABLE,
          method: "get",
          timeout: 8000,
          headers: {
            "Content-Type": "application/json",
          },
        });
        if (res.status == 200) {
          // test for status you want, etc
          // console.log(res.status)
        }
        // Don't forget to return something
        // console.log(res.data)
        // requestData = response.data

        return res.data;
        // Add res.data to requestData
      } catch (err) {
        // Add display error message in vue
        console.error(err);
      }
    },
  },

  mounted() {
    this.fetchData().then((res) => console.log(typeof res));
    // Add test for failed request
  },
};
</script>

<style scoped>
.selected {
  background-color: aqua;
}
</style>
