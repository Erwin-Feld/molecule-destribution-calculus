<template>
  <section>
    <ul>
      <li
        v-for="item in requestData.molecules"
        :key="item.id"
        @click="updateChosenData($event.target)"
      >
        {{ item.name }}
      </li>
    </ul>
   <button @click="clickme">test</button>
  </section>
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";
import axios, { get } from "axios";
import molecules from "../assets/comp.Data/molecules.json";

export default {
  // name: "CalculationSection",
  // list item state 
  data() {
    return {
      chosenData: [],
      requestData: molecules,
    };
  },

  methods: {
    updateChosenData(target) {

      // Add internal state list ?
      // get Index of this li the ul 
      // problem is index ! == id 
      // use Set ?
      const li = target.closest('li');
      const nodes = Array.from( target.closest('ul').children );
      const index = nodes.indexOf( li );
      console.log(index)

      /* user clicked on elem again to unselect */
      /* del dataElm from choosenData */
      if (this.dataElmFound(target)) {
        // deleteDataElm
        this.chosenData.splice(this.choseDataElmIndex(target), 1)
        /* untoggle class */
        target.classList.toggle("selected");
        console.log(this.chosenData)

        /* user selects element */
      } else {
        /* add dataElm to choosenData */
        this.chosenData.push(
          this.requestData.molecules[this.reqDataElmIndex(target)]
        );
        /* toggle class */
        target.classList.toggle("selected");
      }
    },

    /* returns the index position of the matched target elment */
    reqDataElmIndex(target) {
      return this.requestData.molecules.findIndex(
        (elem) => elem.name === target.innerText
      );
    },

    choseDataElmIndex(target){
       return this.chosenData.findIndex(
        (elem) => elem.name === target.innerText
      );
    },

    /* checks if chosenData element already contains that  */
    /* returns true if element found in choosen Data */
    dataElmFound(target) {
      return this.chosenData.some((elm) => elm.name === target.innerText);
    },

    delDataElm() {},

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

    clickme(){
      // execute this function only when this.dataChanges changes data
      

     if(this.dataChange){
       console.log("changed")
     }
    }
  },



  computed: {
    dataChange(){
      console.log("data changed")
      return this.chosenData
    }


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
