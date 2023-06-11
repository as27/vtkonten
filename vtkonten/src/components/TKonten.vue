<script setup>
import { computed } from '@vue/reactivity';
import TKonto from './TKonto.vue'

const props = defineProps({
  buchungen: {
    type: Array
  }
})


//console.log(props)
const kontobuchungen = computed(() => {
  var k = {};
  props.buchungen.forEach(element => {
    if (k[element.ksoll] === undefined) {
      k[element.ksoll] = []
    }
    if (k[element.khaben] === undefined) {
      k[element.khaben] = []
    }
    if (element.btrsoll != "") {
      k[element.ksoll].push({
        tsoll: element.text,
        bsoll: element.btrsoll,
        thaben: '',
        bhaben: ''
      })
    } 
    if (element.btrhaben != "") {
      k[element.khaben].push({
        tsoll: '',
        bsoll: '',
        thaben: element.text,
        bhaben: element.btrhaben
      })
    } 
  });
  delete k[""];
  return k;
});
//console.log(kontobuchungen);


</script>



<template>
  <div class="konten">
    <TKonto v-for="(val, key) in kontobuchungen" :kontoname="key" :buchungen="val" />
  </div>
</template>
