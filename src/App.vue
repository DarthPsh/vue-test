<template>

  <el-row>
    <el-input 
      @input="inputWordsCount"
      @keypress.enter="sortInputValues"
      v-model="input"
      type="text"
      placeholder="Please input"
    ></el-input>
  </el-row>
  
  <el-row>
    <el-button 
    @click="sortInputValues"
    type="primary"
    >Сортировать</el-button>
  </el-row>

  <template 
  v-if="this.inputArr.length">
    <el-row>
      <el-select v-model="value" :placeholder="value">
        <el-option
          v-for="item in sortInputValues()" 
          :key="item"
          :label="toLocaleUpperCase(item)"
          :value="item"
        ></el-option>
      </el-select>
    </el-row>
  </template>


  <div>
    <el-checkbox-group v-model="checkboxGroup">
      <el-checkbox-button
      v-for="num in numbers" 
      :label="num" 
      :key="num"
      >{{num}}</el-checkbox-button>
    </el-checkbox-group>
    <div>Сумма чекбоксов = {{ checkRes }}</div>
  </div>
  

</template>



<script>
import { defineComponent, ref } from 'vue'
export default defineComponent ({
  setup() {
    return {
      input: ref('')
    };
  },
  data() {
    return {
      inputArr: [],
      value: 'Select',
      checkboxGroup: [],
      numbers: [5, 8, 12, 15, 22],
    };
  }, // data
  methods: { 
    inputWordsCount() {
        let words = this.input.split(',');
        words = words.map(x => { return x.trim(); });
        words = words.filter(element => element !== "");
        console.log(words)
        if(words.length == 11) {
          alert('стопэ');
          this.input = words.slice(0, 10).join(',');
        }
    },
    sortInputValues() {
      this.inputArr = this.input;
      return this.inputArr
        .split(",")
        .map(x => { return x.trim(); })
        .sort(function (a, b) {
          return a.localeCompare(b);
        })
        .filter(element => element !== "")
    },
    toLocaleUpperCase(item) {
      return item.toLocaleUpperCase();
    },
  }, // methods
  computed: {
    checkRes() {
    	return this.checkboxGroup.reduce(function (a, b) {
      	return parseInt(a) + parseInt(b);
      }, 0);
    },
  } // computed
})
</script>

<style>
</style>