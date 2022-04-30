// ##############################################################################
// #######             PROJECT NAME : Vue Random Numbers                  #######
// ##############################################################################
//                                Synopsis:
//  Program which allows to generate up to 5 sets of 5 random and unique numbers

<template>
  <div class="container">
    <h1>Your Lucky Numbers</h1>
    <br /><br />

    <div
      class="row justify-content-center"
      v-for="(number, id) in numbers"
      :key="id"
    >
      <div class="col-sm-1 col-md-1 col-xs-12">
        <ul>
          <li  v-for="n in number" :key="n">{{ n }}</li>
        </ul>
        
      </div>
    </div>
    <div class="row justify-content-center" style="margin-top: 2rem">
      <div class="col-2">
        <button @click="generate" class="btn btn-primary">
          Get Your Lucky Numbers
        </button>
      </div>
      <div class="col-3">
        <label for="times">How many sets?</label>
        <select v-model="times">
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
          <option>5</option>
        </select>
      </div>
    </div>
  </div>
</template>

 <script>
import { ref } from "vue";

export default {
  setup() {
    let times = ref(1);
    let numbers = ref({});

    function generate() {
      new generateNew();
    }

   function generateNew() {
    //  declare variables
      let rowNumbers = [];
      let colNumbers = [];
      let numExist = [];
      // outer loop for SETS of numbers
      for (let i = 0; i < times.value; i++) {
        // inner loop for 5 numbers in set
        for (let y = 0; y < 5; ) {
          var r = Math.floor(Math.random() * 48) + 1;
          // validate if number is unique
          numExist = colNumbers.includes(r);
          if (!numExist) {
            colNumbers.push(r);
            y++;
          }
          // sort from smallest to biggest 
          colNumbers.sort(function (a, b) {
            return a - b;
          });
        }
        rowNumbers.push(colNumbers);
        colNumbers = [];
      }
      numbers.value = rowNumbers;
    }

    return {
      numbers,
      generate,
      times,
    };
  },
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
