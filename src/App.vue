<script setup>
  import Card from './components/card.vue';
</script>

<template>
  <div class="grid place-items-center p-5">
      <p v-if="error.length">
        <b class="text-light bg-red px-10 py-3">{{error}}</b>
      </p>
    <div class="sm:flex bg-amber p-5 m-5 border-rounded">
      <div class="flex items-center p-1">
        <div>Generate</div>
        <div class="px-2">
          <input type="text" class="w-9 p-2.5" placeholder="X" v-model="x_count" />
        </div>
        <div>rabdiom cards, </div>
      </div>
      <div class="flex items-center p-1">
        <div>each with</div>
        <div class="px-2">
          <input type="text" class="w-9 p-2.5" placeholder="Y" v-model="y_count" />
        </div>
        <div>row/columns</div>
      </div>
      <div class="p-1">
        <button
          class="px-4 py-2 text-white border rounded"
          :class="[isDisabled ? disabledClass : activeClass]"
          @click="handleInput"
          :disabled="isDisabled"
        >
          Generate
        </button>
      </div>
    </div>
    <div class="border-black border-size-3">
      <Card :x_data="x_temp" :y_data="y_temp" :c_time="on_ctime"/>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        x_count: 5,
        y_count: 5,
        x_temp: 0,
        y_temp: 0,
        on_ctime: 0,
        error: "",
        isDisabled: false,
        activeClass: 'bg-blue-400 hover:bg-blue-500',
        disabledClass: 'bg-grey-400'
      };
    },
    mounted() {
      this.handleInput()
    },
    watch: {
      x_count: function() {
        if ( isNaN(this.x_count) ){
            this.error = "You can only enter number.";
            this.isDisabled = true;
        }else{
          if ( this.x_count > 5 ||  this.x_count < 1 ){
            this.error = "You can only enter 1 ~ 5.";
            this.isDisabled = true;
          } else {
            this.error = "";
            this.isDisabled = false;
          }
        }
      },
      y_count: function() {
        if ( isNaN(this.y_count) ){
            this.error = "You can only enter number.";
            this.isDisabled = true;
        }else{
          if ( this.y_count > 5 ||  this.y_count < 1 ){
            this.error = "You can only enter 1 ~ 5.";
            this.isDisabled = true;
          } else {
            this.error = "";
            this.isDisabled = false;
          }
        }
      }
    },
    methods: {
      handleInput:function(){
        this.x_temp = parseInt(this.x_count);
        this.y_temp = parseInt(this.y_count); 
        this.on_ctime = Date.now();
      }
    },
  };
</script>

<style scoped>
</style>
