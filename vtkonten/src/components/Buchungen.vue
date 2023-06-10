<script setup>
import { computed } from '@vue/reactivity';
import { ref } from 'vue'

const props = defineProps(['modelValue'])
defineEmits(['update:modelValue'])

const kontendef = ref("Bank,Kasse")

const konten = computed(() => {
  return kontendef.value.split(",");
});

const buchungen = ref([
  {
    text: '',
    ksoll: '',
    btrsoll: '',
    khaben: '',
    btrhaben: ''
  }
])
function addRow() {
  props.modelValue.push({
    text: '',
    ksoll: '',
    btrsoll: '',
    khaben: '',
    btrhaben: ''
  })
}
</script>

<template>
  <input v-model="kontendef" />
  <table>
    <tr>
      <th>Text</th>
      <th>Soll</th>
      <th>Betrag</th>
      <th></th>
      <th>Haben</th>
      <th>Betrag</th>
    </tr>
    <tr v-for="buchung in modelValue">
      <td><input v-model="buchung.text" />

      </td>
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
    </tr>
  </table>

  <a @click="addRow">Add row</a>
</template>

<style scoped>
input {
  width: 80%;
}

.btr input {
  width: 60px;
  text-align: right;
}
</style>
