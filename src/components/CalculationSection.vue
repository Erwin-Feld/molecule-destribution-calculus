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
  name: "CalculationSection",
  setup() {
    let requestData = ref(molecules);

    /* do not need to be reactive */
    let selectedElements = ref([]);

    async function fetchData() {
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
      } catch (err) {
        // Add display error message in vue
        console.error(err);
      }
    }

    function toggleClass(target) {
      target.classList.toggle("selected");
      selectedElements.value.push(3);
      console.log(selectedElements.value)
    }

    onMounted(() => {
      fetchData()
        // Add test for failed request
        .then((res) => console.log(typeof res));
    });

    return {
      requestData,
      fetchData,
      toggleClass,
      selectedElements
    };
  },
};
</script>

<style scoped>
.selected {
  background-color: aqua;
}
</style>
