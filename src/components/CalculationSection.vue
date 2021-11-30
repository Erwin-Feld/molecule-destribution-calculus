<template>
  <section>
    <ul>

      <li v-for="item in requestData.molecules" :key="item.id"
      @click="toggleClass($event.target)"
      
      >{{item.name}}</li>
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
     let selectedElements =ref([1,2,3]);

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

    /* add/remove class on click */
    function toggleClass(target){
           target.classList.toggle('selected')
          console.log(selectedElements.value)


          // look if something changes
          // button click if the values are changing 

        // I want to know if the value changes 
      // set it reactive 
      // 


          //  if target.innterText is inside selecteD Elements
          // remove it 

          // else add it 



      // console.log(target.innerText)
      // if target.innerText is also matches 
      // 


      // for(let element of requestData._rawValue.molecules) {
       

      //   if(selectedElements.some(el=> el.name === element.name)){
      //     console.log(`match ${element.name}`)


      //   }


      //   else if(target.innerText === element.name){
      //     // console.log(element)
      //     // Add to calc
      //     // update the selectedElements array
      //     selectedElements.push(element)
      //     // console.log(selectedElements)
      //     target.classList.toggle('active')

      //     return true

          // selectedElements.push(i)
          
          // console.log(i)
        
        // console.log(i)
 
      
      // console.log(requestData._rawValue.molecules)
      // add that text to it 
      // 
    }


    


    onMounted(() => {
      fetchData()
        // Add test for failed request
        .then((res) => console.log(typeof res));
    });

    return {
      requestData,
      toggleClass,
      
    };
  },
};
</script>


<style scoped>

.selected {
  background-color: aqua;
}

</style>