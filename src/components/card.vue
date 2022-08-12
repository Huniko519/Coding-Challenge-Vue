<script setup>
import { ref } from 'vue';

defineProps({
  x_data: Number,
  y_data: Number,
  c_time: Number,
});
const count = ref(0); 

</script>
<template>
  <div
    v-for="(val, index) in getcardValues"
    :key="index"
  >
    <div
      v-for="(valss, v_index) in val"
      :key="v_index"
      class="border-black border-size-3 inline-grid text-center text-size-4xl font-bold w-16 h-16"
    >
      {{valss}}
    </div>
  </div>
</template>

<script>
export default {
  functional: true,
  props: ['x_data', 'y_data', 'c_time'],
  data() {
    return {
      cards: []
    }
  },
  computed: {
    getcardValues() {
      return this.cards
    }
  },
  watch: { 
    c_time: function() {
      var result           = [];
      var characters       = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      var length = this.x_data * this.y_data;
      var chunk = [];
      for ( var i = 0; i < length; i++ ) {
        var rand = characters.charAt(Math.floor(Math.random() * characters.length));
        characters = characters.replace(rand, '');
        chunk.push(rand);
        if ( chunk.length == this.x_data ){
          result.push(chunk);
          chunk = [];
        }
      }
      this.cards = result;
    }
  }
}
</script>

<style scoped>
</style>
