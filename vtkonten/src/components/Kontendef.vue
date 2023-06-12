<script setup>
import { computed } from '@vue/reactivity'
import { ref } from 'vue'

const props = defineProps(['modelValue'])
defineEmits(['update:modelValue'])

const kontendef = ref('Bank,Kasse')

function emitValue(e) {
  emit('update:modelValue', kontendef.value.split(','))
}

/*
TODO: Refactoring bzgl. auslagerung von Kontendefinierung

*/
</script>

<template>
  Konten:
  <input v-model="kontendef" @input="emitValue" />
</template>

<style scoped>
input {
  width: 150px;
}
</style>
