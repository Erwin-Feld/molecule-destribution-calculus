<template>
  <input type="text" v-model="userInput" />
  <button @click="printValue">change</button>
  <p></p>
</template>

<script>
import { watch, ref } from "@vue/runtime-core";

export default {
  setup() {
    const userInput = ref("");

    const dataChangeFlag = ref(false);

    function printValue(){
        console.log("executed click")
        if(dataChangeFlag.value){
            console.log("doeng stuff")

            dataChangeFlag.value = false;
            console.log(dataChangeFlag.value)
        }
    }

        watch([userInput], (newValues, prevValues) => {
      if (newValues) {
          console.log(newValues)
        dataChangeFlag.value = true;
      }
    });

    //  watch([userInput], (newValues, prevValues) => {
    //   if (newValues) {
    //       console.log(newValues)
    //     return true;
    //   }
    // });

    return {
      userInput,
      printValue,
      dataChangeFlag
     
    };
  },
};


</script>

