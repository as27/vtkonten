<script setup>
import { ref } from 'vue'

import Buchungen from './components/Buchungen.vue'
import TKonten from './components/Tkonten.vue'
import Kontendef from './components/Kontendef.vue';


const buchungen = ref([
  {
    zeile: 1,
    text: '',
    ksoll: '',
    btrsoll: '',
    khaben: '',
    btrhaben: '',
    color: ''
  }
])


</script>

<template>
  <main>

    <Buchungen v-model="buchungen" />
    <TKonten :buchungen="buchungen" />
    
  </main>
</template>

<style scoped></style>
