<script setup>
import { computed } from '@vue/reactivity'
import { ref } from 'vue'

const props = defineProps(['modelValue'])
defineEmits(['update:modelValue'])

const kontendef = ref('Bank,Kasse')

const nextIndex = ref(2)

const konten = computed(() => {
  return kontendef.value.split(',')
})

const farben = ref([
  { val: '', name: '' },
  { val: '#D3D3D3', name: 'grau' },
  { val: '#FFFACD', name: 'gelb' },
  { val: '#ADD8E6', name: 'blau' },
  { val: '#f5c1c1', name: 'rot' },
  { val: '#90EE90', name: 'grün' }
])

function addRow() {
  props.modelValue.push({
    zeile: nextIndex.value,
    text: '',
    ksoll: '',
    btrsoll: '',
    khaben: '',
    btrhaben: '',
    color: ''
  })
  nextIndex.value++
}

function deleteRow(index) {
  console.log('delete' + index)
  props.modelValue.splice(index, 1)
}
</script>

<template>
  <input v-model="kontendef" size="80" />
  <table>
    <tr>
      <th>Zeile</th>
      <th>Text</th>
      <th>Soll</th>
      <th>Betrag</th>
      <th></th>
      <th>Haben</th>
      <th>Betrag</th>
      <th>Farbe</th>
      <th></th>
    </tr>
    <tr v-for="(buchung, bzeile) in modelValue" :style="{ 'background-color': buchung.color }" >
      <td class="zeile"><input v-model="buchung.zeile" /></td>
      <td class="text"><input v-model="buchung.text" /></td>
      <td>
        <select v-model="buchung.ksoll">
          <option v-for="k in konten">{{ k }}</option>
        </select>
      </td>
      <td class="btr"><input v-model="buchung.btrsoll" /></td>
      <td>an</td>
      <td>
        <select v-model="buchung.khaben">
          <option v-for="k in konten">{{ k }}</option>
        </select>
      </td>
      <td class="btr"><input v-model="buchung.btrhaben" /></td>
      <td>
        <select v-model="buchung.color">
          <option v-for="f in farben" :value="f.val">{{ f.name }}</option>
        </select>
      </td>
      <td><a @click="deleteRow(bzeile)"><img width="14" height="14" src="./../assets/minus.svg" /></a></td>
    </tr>
  </table>
  <img @click="addRow" width="14" height="14" src="./../assets/plus.svg" />&nbsp;
  <a @click="addRow">Add row </a>
</template>

<style scoped>

input,select {
  background-color: transparent;
}
.text input {
  width: 150px;
}

.zeile input {
  width: 20px;
  text-align: center;
}

.btr input {
  width: 60px;
  text-align: right;
}
</style>
