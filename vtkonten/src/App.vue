<script setup>
import { ref } from 'vue'

import Buchungen from './components/Buchungen.vue'
import TKonten from './components/Tkonten.vue'
import Kontendef from './components/Kontendef.vue';

const buchungen = ref([
  {
    text: '',
    ksoll: '',
    btrsoll: '',
    khaben: '',
    btrhaben: ''
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
