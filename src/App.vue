<template>
  <div class="w-screen h-screen justify-center items-center flex">
    <!-- App -->
    <div class="w-[35%] bg-slate-500 h-3/4 flex flex-col">
      <!-- Display -->
      <div class="m-5 mb-0 w-[1/2] h-22 bg-white drop-shadow-lg p-2">
        <h1 class="text-5xl float-right"> {{!display ? '0' : display }}</h1>
      </div>
      <!-- End: Display -->
      <!-- Keys -->
      <div class="m-5 h-full w-[1/2] grid grid-rows-5 grid-cols-4 gap-5 p-2">
        <template v-for="key in keysName">
          <Key @click="keyClicked(key)" value='keyClick'>{{ key }}</Key>
        </template>
      </div>
    </div>
  </div>
  <!-- End: App -->
</template>

<script>
import Key from './components/Key.vue';

export default {
  name: 'App',
  data() {
    return {
      keysName: ['AC', '%', '√', '÷',9, 8, 7, 'x', 6, 5, 4, '-', 3, 2, 1, '+', 0, '00', '.', '='],
      display: '',
      operatorClick: false,
      prevNum: '',
      currentNum: '',
      result: '',
      operator: null,
    }
  },
  components: {
    Key 
  },
  methods: {
    keyClicked(keyValue) {

      if(keyValue == 'AC') {
        this.display = '';
        this.prevNum = '';
        this.currentNum = '';
        this.operatorClick = false;
        this.result = '';
        this.operator = null;
      }
      
      //append the click number
      if(!isNaN(keyValue) && this.operatorClick == false ) {
        this.display += keyValue;
      }else if(!isNaN(keyValue) && this.operatorClick == true) {
        this.currentNum += keyValue.toString();
        this.display = this.currentNum;
      }

      //plus click
      if(keyValue == '+') {

        if(this.operatorClick == true) {
          this.result = Number(this.prevNum) + Number(this.currentNum);
          this.display = this.result;
          this.prevNum = this.result;
          this.currentNum = '';
        }
        
        this.prevNum = this.display;
        this.operatorClick = true;
        this.operator = '+';
        
      }

      // minus click
      if(keyValue == '-') {
        if(this.operatorClick == true) {
          this.result = Number(this.prevNum) - Number(this.currentNum);
          this.display = this.result;
          this.prevNum = this.result;
          this.currentNum = '';
        }
        
        this.prevNum = this.display;
        this.operatorClick = true;
      }

       // times click
       if(keyValue == 'x') {
        if(this.operatorClick == true) {
          this.result = Number(this.prevNum) * Number(this.currentNum);
          this.display = this.result;
          this.prevNum = this.result;
          this.currentNum = '';
        }
        
        this.prevNum = this.display;
        this.operatorClick = true;
      }

       // divide click
       if(keyValue == '÷') {
        if(this.operatorClick == true) {
          this.result = Number(this.prevNum) / Number(this.currentNum);
          this.display = this.result;
          this.prevNum = this.result;
          this.currentNum = '';
        }
        
        this.prevNum = this.display;
        this.operatorClick = true;
      }

      //equals click 
      if(keyValue == '=') {
        this.total = this.prevNum + this.operator + this.currentNum;
        this.display = eval(this.total);
        this.operator = null;
      }

      if(keyValue == '%') {
        this.total = Number(this.display) / 100;
        this.display = this.total;
      }

      if(keyValue == '√') {
        this.total = Math.sqrt(Number(this.display));
        this.display = this.total;
      }
    }
  },
}
</script>

<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>
